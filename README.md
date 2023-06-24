# Description

Reuseable Github Workflows. This allows to maintain workflows commonly used in repos in a central location.
When a workflow changes, or the support matrix, it can be changed only once for all dependent repos

## Workflow : ansible_role_molecule

Workflow called for molecule testing when creating a pull request on branch main.
Tested operating systems:
- Debian 10
- Debian 11
- Debian 12
- Centos Stream 8
- Rocky Linux 9

Tested against python versions:
- 3.9
- 3.10
- 3.11

```yaml
---
name: Molecule Test
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  call-workflow-molecule:
    uses: infra-monkey/reuseable_workflows/.github/workflows/ansible_role_molecule.yml@main
    with:
      role-name: 'my_role' # The role name as defined in meta/main.yml
```

## Workflow : ansible_role_release

Workflow called when a new release is defined in the repo.

```yaml
---
name: Release
'on':
  push:
    tags:
      - '*'

jobs:
  call-workflow-release:
    uses: infra-monkey/reuseable_workflows/.github/workflows/ansible_role_release.yml@main
    secrets:
      GALAXY_API_KEY: ${{ secrets.GALAXY_API_KEY }} # Github secret containing the ansible galaxy api key linked to your galaxy account
```
