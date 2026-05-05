[![Clone Public Repository Workflow](https://github.com/fonestardev/checkout/actions/workflows/public-repo.yml/badge.svg)](https://github.com/fonestardev/checkout/actions/workflows/public-repo.yml)

# Clone Github Repository Action with Private Submodule

Github Action to clone a **public** or **private** Github repository and access its content on others repositories' workflows that include private submodules.

Supports **Linux**, **macOS**, and **Windows** runners.

## How to use this action?

Create a new `.yml` file on your `.github/workflows` directory.

Field | Mandatory | Observation
------------ | ------------  | -------------
**repository** | YES | Ex: `fonestar/checkout` | 
**branch** | NO | Ex: `main` (default: resolved from event context)
**depth** | NO | Ex: `1` (most recent commit only)
**submodule** | NO | `false` or `true`
**path** | NO | Relative path under `$GITHUB_WORKSPACE` to place the repository (default: `.`)
**access-token** | NO | [How to create a PAT](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token)
**actor** | NO | Ex: username

### For a public repository (with depth)

```yaml
- name: Clone fonestardev/checkout PUBLIC repository
  uses: fonestardev/checkout@master
  with:
    depth: 1
    branch: 'master'
    repository: 'fonestardev/fonestar-unity'
```

### For a private repository

To use this action to clone a `PRIVATE` repository the Github User/Admin has access to, it's necessary to create a [PERSONAL ACCESS TOKEN](https://github.com/settings/tokens) with `REPOSITORY` scopes.

```yaml
- name: Clone fonestardev/audio-testing PRIVATE repository
  uses: fonestardev/checkout@master
  with:
    repository: 'fonestardev/audio-testing'
    access-token: ${{ secrets.ACCESS_TOKEN }}
```

### Clone into a specific path

Use the `path` input to place the cloned repository in a subdirectory of `$GITHUB_WORKSPACE`:

```yaml
- name: Clone into a subdirectory
  uses: fonestardev/checkout@master
  with:
    repository: 'fonestardev/fonestar-unity'
    path: 'libs/fonestar-unity'
```

### Windows runner support

This action works on `windows-latest` runners without any extra configuration. The action automatically detects the OS and runs the appropriate shell (PowerShell on Windows, bash elsewhere).

```yaml
jobs:
  build:
    runs-on: windows-latest
    steps:
      - name: Clone repository
        uses: fonestardev/checkout@master
        with:
          repository: 'fonestardev/fonestar-unity'
          access-token: ${{ secrets.ACCESS_TOKEN }}
```

### Access repository content

After using this action in your workflow, you can use the following command to access the cloned repository content:

**Linux / macOS**
```bash
- name: Access cloned repository content
  run: |
    cd <repository-name>
    ls -la
```

**Windows**
```yaml
- name: Access cloned repository content
  shell: pwsh
  run: |
    Set-Location <repository-name>
    Get-ChildItem
```

## Licensed

☞ This repository uses the [Apache License 2.0](https://github.com/fonestardev/aws-cliaction/blob/main/LICENSE)

