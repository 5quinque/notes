# Python

## Setting up virtual environments

### pipenv

https://realpython.com/pipenv-guide/

Install pipenv

```bash
pip install pipenv
```

Spawn a shell in a virtual environment

```bash
pipenv shell
```

Install a package

```bash
pipenv install XXX
```

### virtualenvwrapper

https://virtualenvwrapper.readthedocs.io/en/latest/install.html

```bash
pip install virtualenvwrapper
```

## Pre commit hooks

```bash
pipenv install pre-commit
```

File : `.pre-commit-config.yaml`

```
repos:
  - repo: https://github.com/timothycrosley/isort
    rev: 5.9.3
    hooks:
    - id: isort
      files: .*.py$
  - repo: https://github.com/psf/black
    rev: 21.7b0
    hooks:
    - id: black
  - repo: https://github.com/pycqa/flake8
    rev: 3.9.2
    hooks:
    - id: flake8
```

`pre-commit install`




