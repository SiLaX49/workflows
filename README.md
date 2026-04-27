# workflows

Workflows GitHub Actions réutilisables pour mes projets.

## `python-ci.yml`

Pipeline CI Python : lint (ruff) + tests (pytest) + build Docker.

### Utilisation

Dans n'importe quel repo, créer `.github/workflows/ci.yml` :

```yaml
name: CI
on: [push, pull_request]

jobs:
  ci:
    uses: SiLaX49/workflows/.github/workflows/python-ci.yml@main
```

### Avec options

```yaml
jobs:
  ci:
    uses: SiLaX49/workflows/.github/workflows/python-ci.yml@main
    with:
      python-version: "3.11"
      run-docker-build: false
      run-lint: true
      run-tests: true
```
