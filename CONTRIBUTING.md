# Contributing
## Setup
#### Create the python virtual environment
```bash
python -m venv .venv
```

#### Activate the environment

**bash/zsh**

```
source .venv/bin/activate
```

**powershell**
```powershell
.venv/bin/activate.ps1
```

#### Install dependencies
```bash
pip install -r requirements.txt
pre-commit install
```

## Develop
#### Run linting
**Via pre-commit**
```bash
pre-commit run --all-files
```

**Manually**
```bash
yamllint .

anisble-lint main.yaml
ansible-lint

ansible-playbook --syntax-check -i inventory/hosts main.yaml
```
