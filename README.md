# Terraform Beginner Bootcamp 2023

## Semantic Versioning :mage:

This project is going utilize semantic versioning for its tagging.
[semver.org](https://semver.org/)

The general format:

 **MAJOR.MINOR.PATCH**, eg. 1.0.1

- **MAJOR** version when you make incompatible API changes
- **MINOR** version when you add functionality in a backward compatible manner
- **PATCH** version when you make backward compatible bug fixes

## Install the Terraform CLI

### Considetaions with the Terraform CLI changes
The terraform CLI installation instractions have changed due to gpg keyring changes. So we needed refer to latest install CLI instractions via Terraform Documantation and change the scrpiting for install. 

[Install Terraform CLI](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)

### Considerations for Linux Distribution

This project is built against Ubuntu. Please consider checking linux Distribution and change  accordingly needs.
[How to check OS  version on linux](https://www.cyberciti.biz/faq/how-to-check-os-version-in-linux-command-line/
)

Example of checking Verison of Lİnux
```sh
$ cat /etc/os-release
PRETTY_NAME="Ubuntu 22.04.3 LTS"
NAME="Ubuntu"
VERSION_ID="22.04"
VERSION="22.04.3 LTS (Jammy Jellyfish)"
VERSION_CODENAME=jammy
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=jammy
``` 

### Refactoring into bash Scripts

While fixing the terraform CLI gpg depreciation  issues we notice that bash script steps were a considerable amount more code. So we deiceded tı create a bash script to install the Terraform CLI 

This bash sript lacated here : [./bin/install_terraform_cli](./bin/install_terraform_cli)

- This will keep the Gidpod Task File ([.gitpod.yml](.gitpod.yml)) tidy
- Tjis allow us an easir to debug execute manually Terrarform CLI install
- This will allow better portabilty for other project neet to install CLI

### Shebang Considerations
[Shebang](https://en.wikipedia.org/wiki/Shebang_(Unix))

``` 
#! /usr/bin/env bash
``` 

https://en.wikipedia.org/wiki/Chmod
https://www.gitpod.io/docs/configure/workspaces/tasks

### Linux Permissions Considerations
In order to make our bash scripts executable we need to change linux permission for the fix to be exetuable at the user mode.
``` 
chmod u+x ./bin/install_terraform_cli
``` 
alternatively:

``` 
chmod 744 ./bin/install_terraform_cli
``` 
https://en.wikipedia.org/wiki/Chmod

### Github Lifecycle (Before, Init, Command)
We need to be careful when using the Init because it will not rerun if we restart an existing workspace.

https://www.gitpod.io/docs/configure/workspaces/tasks