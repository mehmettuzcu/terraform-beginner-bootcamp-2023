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


# Working Env Vars

#### env command
We can list out all Enviroment Variables (Env Vars) using the `env` command

We can filter specific env vars using grep eg. `env | grep AWS_`

#### Setting and Unsetting Env Vars
In the terminal we can set using `export HELLO='world`

In the terrminal we unset using `unset HELLO`

We can set an env var temporarily when just running a command

```sh
HELLO='world' ./bin/print_message
```
Within a bash script we can set env without writing export eg.

```sh
#!/usr/bin/env bash

HELLO='world'

echo $HELLO
```

Printing Vars
We can print an env var using echo eg. echo $HELLO

#### Scoping of Env Vars
When you open up new bash terminals in VSCode it will not be aware of env vars that you have set in another window.

If you want to Env Vars to persist across all future bash terminals that are open you need to set env vars in your bash profile. eg. `.bash_profile`

#### Persisting Env Vars in Gitpod
We can persist env vars into gitpod by storing them in Gitpod Secrets Storage.

```sh
gp env HELLO='world'
```

All future workspaces launched will set the env vars for all bash terminals opened in thoes workspaces.

You can also set en vars in the `.gitpod.yml` but this can only contain non-senstive env vars.