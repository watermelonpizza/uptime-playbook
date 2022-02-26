<h1 align="center">
  Ansible Playbook Template Repo
</h1>
<p align="center">
  🚧 A repo designed as a template for creating ansible playbook repos
</p>

> Anything with the 🚧 emoji should be removed or replaced with more relevant details in the downstream repo.

### 🚧 Features
- linting using [yamllint](https://github.com/adrienverge/yamllint), [anisble-lint](https://github.com/ansible-community/ansible-lint) and ansibles built in [syntax-check](https://docs.ansible.com/ansible/latest/user_guide/playbooks_intro.html#verifying-playbooks)
- [pre-commit](https://pre-commit.com/) hooks to run linting before commits
- github actions ci to run linting on pr/pushes
- base inventory variable folder structure inspired by the [matrix ansible playbook](https://github.com/spantaleev/matrix-docker-ansible-deploy) repo


## Getting the playbook
This Ansible playbook is meant to be executed on your own computer.

You can retrieve the playbook's source code by:

- [Using git to get the playbook](#using-git-to-get-the-playbook) (recommended)

- [Downloading the playbook as a ZIP archive](#downloading-the-playbook-as-a-zip-archive) (not recommended)


### Using git to get the playbook

Using [git](https://git-scm.com/) is the best way to get the playbook as any updates can be pulled down easily using the `git pull` command.

To download the playbook using `git` run:
```bash
git clone https://github.com/🚧
```

### Downloading the playbook as a ZIP archive

Alternatively, you can download the playbook as a ZIP archive. (not recommended)

The latest version is always at the following URL: https://github.com/🚧

You can extract this archive anywhere.

## Configuration

To configure the playbook before running it there is two things you need to do:

- Set the [inventory](#inventory) file to tell ansible what machines you want to control

- Set any [variables](#variables) you wish to change from their defaults

### Inventory
You will need to add your target hosts to the inventory file.

Copy the example inventory file from `examples/hosts` (`cp examples/hosts inventory/hosts`). Edit to your liking.

### Variables
> ⚠️ You should be familiar with variable precedence in ansible. See [Tips on where to set variables](https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html#tips-on-where-to-set-variables) and [Variable precedence: Where should I put a variable?](https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html#variable-precedence-where-should-i-put-a-variable) ansible guides for an idea where you should put your variable overrides

To configure this playbook you should override as-needed variables in the following places, from least to greatest precedence:
- in the `inventory/hosts` file (not recommended)

- in the `group_vars/all` file to target everything

- in `group_vars/<inventory_group_name>/vars.yaml` to target specific hosts in a group

- in `host_vars/<inventory_host_name>/vars.yaml` to target a single host

In all cases, these files are ignored by git to ensure no secrets are commited to the repo.

> 🚧<br>
> An example of a way to represent variables
> #### Configurable variables
>
> This sets the username which will be created to run myapp
> ```yaml
> application_username: myapp
> ```


## Installation
Once you have [configured](#configuration) the playbook, you can start running the playbook.

Run this command to run the playbook

```
ansible-playbook -i inventory/hosts main.yml
```

## Contribute

See [Contributing](CONTRIBUTING.md)
