<h1 align="center">
  Uptime Kuma + Traefik Playbook
</h1>
<p align="center">
  This repo contains a playbook which will install uptime kuma and traefik as a reverse proxy onto a debian system
</p>

## Getting the playbook
This Ansible playbook is meant to be executed on your own computer.

You can retrieve the playbook's source code by:

- [Using git to get the playbook](#using-git-to-get-the-playbook) (recommended)

- [Downloading the playbook as a ZIP archive](#downloading-the-playbook-as-a-zip-archive) (not recommended)


### Using git to get the playbook

Using [git](https://git-scm.com/) is the best way to get the playbook as any updates can be pulled down easily using the `git pull` command.

To download the playbook using `git` run:
```bash
git clone https://github.com/watermelonpizza/uptime-playbook
```

### Downloading the playbook as a ZIP archive

Alternatively, you can download the playbook as a ZIP archive. (not recommended)

The latest version is always at the following URL: https://github.com/watermelonpizza/uptime-playbook/archive/refs/heads/main.zip

You can extract this archive anywhere.

## Configuration

To configure the playbook before running it there is two things you need to do:

- Set the [inventory](#inventory) file to tell ansible what machines you want to control

- Set any [variables](#variables) you wish to change from their defaults

### Inventory
You will need to add your target hosts to the inventory file.

Copy the example inventory file from `examples/hosts` (`cp examples/hosts inventory/hosts`). Edit to your liking.

### Variables

**To get started**

Copy the example vars file from `examples/vars.yaml` (`cp examples/vars.yaml inventory/<YOUR HOST LOCATION>/vars.yaml`). Edit to your liking.

<hr>

> ⚠️ You should be familiar with variable precedence in ansible. See [Tips on where to set variables](https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html#tips-on-where-to-set-variables) and [Variable precedence: Where should I put a variable?](https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html#variable-precedence-where-should-i-put-a-variable) ansible guides for an idea where you should put your variable overrides

To configure this playbook you should override as-needed variables in the following places, from least to greatest precedence:
- in the `inventory/hosts` file (not recommended)

- in the `group_vars/all` file to target everything

- in `group_vars/<inventory_group_name>/vars.yaml` to target specific hosts in a group

- in `host_vars/<inventory_host_name>/vars.yaml` to target a single host

In all cases, these files are ignored by git to ensure no secrets are commited to the repo.

<hr>

### Configurable Variables

#### Nodejs

|variable|required|default|description|
|--------|--------|-------|-----------|
|`nodejs_version`|optional|`16.x`|Version of nodejs to install for uptime kuma|

#### Traefik

If `traefik_enable_https` is enabled you must have the conditionally required variables set.

|variable|required|default|description|
|--------|--------|-------|-----------|
|`traefik_user`|optional|`traefik`|The linux username that the traefik process will run under|
|`traefik_version`|optional|`v2.6.1`|The version of traefik to use|
|`traefik_architecture`|optional|`amd64`|The architecture of the machine which traefik will be running under (see the [traefik release assets](https://github.com/traefik/traefik/releases) to see what is available, set `armv7` for raspberry pi|
|`traefik_home`|optional|`/var/www`|Where the home directory of the traefik user is|
|`traefik_config_directory`|optional|`/etc/traefik`|Location of the traefik config files|
|`traefik_enable_https`|optional|``|Whether to enable https (requires below to be set if true|
|`traefik_acme_email`|**conditionally required**||Email address used for letsencrypt|
|`traefik_cloudflare_dns_token`|**conditionally required**||Token to allow letsencrypt to verify domains|

#### Uptime Kuma

|variable|required|default|description|
|--------|--------|-------|-----------|
|`uptime_kuma_domain`|**required**||The BARE domain which uptime kuma is located at. E.g. `up.mydomain.com`|
|`uptime_kuma_user`|optional|`uptime`|The linux username that the uptime kuma nodejs process will run under|
|`uptime_kuma_version`|optional|`1.12.1`|The git-tagged version of uptime kuma to clone|
|`uptime_kuma_home`|optional|`/home/uptime`|Where the home directory of the `uptime_kuma_user` is|
|`uptime_kuma_installation_directory`|optional|`{{ uptime_kuma_home }}/uptime-kuma`|Directory of the uptime kuma installation|

## Installation

Once you have [configured](#configuration) the playbook, you can start running the playbook.

Run this command to run the playbook (you might need `-K` to ask for become (sudo) password)

```
ansible-playbook -i inventory/hosts main.yaml
```

## Contribute

See [Contributing](CONTRIBUTING.md)
