# Terraform Beginner Bootcamp 2023

## Semantic Versioning! :mage:

This project is going to utilize semantic versioning for its tagging.
https://semver.org/

The general format:

 **MAJOR.MINOR.PATCH**, eg. 1.0.1

- **MAJOR** version when you make incompatible API changes
- **MINOR** version when you add functionality in a backward compatible manner
- **PATCH** version when you make backward compatible bug fixes


## Install the Terraform CLI

## Considerations with the Terraform CLI changes

The Terraform CLI installation instructions have changed do to gpg keyring changes. So we needed to refer to the latest install CLI instructions via Terraform Documentation and change the scripting for install.

[Install Terraform CLI] (https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)


### Considerations for Linux Distribution

This project is built against Ubunutu. 
Please consider checking your Linux distribution and change accordingly to your distribution needs. 

[HOw to Check OS Version in Linux]()
https://www.cyberciti.biz/faq/how-to-check-os-version-in-linux-command-line/)

### Refactoring into Bash Scripts

While fixing the Terraform CLI gpg depreciation issues we noticed that bash scripts steps were a considerable amount more code. So we decided to create a bash script to install the Terraform CLI. 

This bash script is located here: [.bin/install_terraform_cli]

-This will keep the Gitpd Task file ([].gitpod.yml]) tidy. 
-This will allow us an easier time to debug and execute manually Terraform CLI install. 
-This will allow better portability for other projects that need to install Terraform CLI. 



https://en.wikipedia.org/wiki/Shebang_(Unix)

https://en.wikipedia.org/wiki/Chmod
https://www.gitpod.io/docs/configure/workspaces/workspace-lifecycle


### Working Env Vars

We can list out all Environment Variables (Env Vars) using the 'env' command

We can filter specific env vars using grep eg. 'env | grep AWS_'f