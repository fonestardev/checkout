[![Clone Public Repository Workflow](https://github.com/fonestardev/checkout/actions/workflows/public-repo.yml/badge.svg)](https://github.com/fonestardev/checkout/actions/workflows/public-repo.yml)

# Clone Github Repository Action with Private Submodule

Github Action to clone a **public** or **private** Github repository and access its content on others repositories' workflows that include private submodules.

## How to use this action?

Create a new `.yml` file on your `.github/workflows` directory.

Field | Mandatory | Observation
------------ | ------------  | -------------
**repository** | YES | Ex: `fonestar/checkout` | 
**branch** | NO | Ex: `main` (default)
**depth** | NO | 1 `Ex: most recent commit`
**submodule** | NO | `false` or `true`
**access-token** | NO | [How to create a PAT](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token)
**actor** | NO | Ex: username

### For a public repository (with depth)

```bash
- name: Clone fonestardev/checkout PUBLIC repository
  uses: fonestardev/checkout@master
  with:
    depth: 1
    branch: 'master'
    repository: 'fonestardev/fonestar-unity'
```

### For a private repository

To use this action to clone a `PRIVATE` repository the Github User/Admin has access to, it's necessary to create a [PERSONAL ACCESS TOKEN](https://github.com/settings/tokens) with `REPOSITORY` scopes.

```bash
- name: Clone fonestardev/audio-testing PRIVATE repository
  uses: fonestardev/checkout@master
  with:
    repository: 'fonestardev/audio-testing'
    access-token: ${{ secrets.ACCESS_TOKEN }}
```

### Access repository content

After using this action in your workflow, you can use the following command to access the cloned repository content:

```bash
cd <repository-name>
```

#### Step Example

```bash
- name: Access cloned repository content
  run: |
    cd <repository-name>
    ls -la
```

## Licensed

☞ This repository uses the [Apache License 2.0](https://github.com/fonestardev/aws-cliaction/blob/main/LICENSE)

