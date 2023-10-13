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

### ENV Command

We can list out all Environment Variables (Env Vars) using the `env` command

We can filter specific env vars using grep eg. `env | grep AWS_`

### Setting and Unsetting Env Vars

In the terminal we can set using `export HELLO=world`

In the terminal we can unset using `unset HELLO`

We can set an env var temporarily when just running a command

```sh
HELLO='world' ./bin/print_message
```

Within a bash script we can set env without writing export eg.

```sh
#!/usr/bin/env.bash

HELLO='world'

echo $HELLO
```  

#### Printing Env Vars

We can print an env var using echo eg. `echo $HELLO`

##### Scoping of Env Vars
 When you open up a new bash terminal in VSCode it will not be aware of env vars that you have set in another window. 

 If you want Env Vars to persist across all future bash terminals that are open you need to set env vars in your bash profile. `.bash_profile`


#### Persisting Env Vars in Gitpod

WE can persist env vars into gitpod by storing them in Gitpod Secrets Storage. 

```
gp env HELLO='world'
```

All future workspaces launched will set the env vars for all bash terminals opened in those workspaces. 

You can also set env vars in the `.gitpod.yml` but this can only contain non-sensitive env vars.

## Terraform Basics

### Terraform Registry

Terraform sources their providers and modules from the Terrform registry which located at [registry. 
Terraform.io](https://registry.terraform.io/)

- **Providers** is an interface to AIs that will allow you to create recources in terraform. 
- **Modules** are a way to make large amounts of terraform code modular, portable and shareable. They are templates. 

[Random Terraform Provider](https://registry.terraform.io/providers/hashicorp/random)

#### Terraform Console

We can see a list of all the Terraform commands by simply typing `terraform`

##### Terraform Init

At the start of a new terraform project we will run `terraform init` to download the binaries for the terraform providers that we'll use in this project. 

###### Terraform Plan

`terraform plan`

This will generate out a changeset, about the state of our infrastructure and what will be changed. 

We can out put this changset ie. "plan" to be passed to an apply, but often you can just ignore outputting. 

###### Terraform Apply

`terraform apply`

This will run a plan and pass the changeset to be execute by terraform. Apply should prompt yes or no. 

If we want to automatically approve an apply we can provide the auto approve flag eg. `terraform apply --auto-approve `

### Terraform Destroy

`terraform destroy`
This will destroy resources.

If we want to automatically approve an apply we can provide the auto approve flag eg. `terraform apply --auto-approve `

## Terraform Lock Files

`.terraform.lock.hcl` contains the locked versioning for the providers or modules that should be used with this project. 

The Terraform Lock File should be commited to your Version Control System (VCS) eg. Github

### Terraform State Files

`.terraform.tfstate` contains information about the current stat of your infrastructure. 

This file **Should not be commited** to your VCS. 

This file can contian sensative data. 

If you lose this file, you lose knowing the state of your infrastructure. 

`.terraform.tfstate.backup` is the previous state file state. 

### Terraform Directory

`.terraform` directory contains binaries of terraform providers.

 ## Issues with Terraform Cloud and Gitpod Workspace

 When attempting to run `terraform login` it will launch in bash a wiswig view to generate a token. However, it does not work as expected in Gitpod VsCode in the brower. 

 The workaround is to manually generate a token in Terraform Cloud

 ```
 https://app.terraform.io/app/settings/tokens?source=terraform-login
 ```

Then create the file manually here:
```sh
touch /home/gitpod/.terraform.d/credentials.tfrc.json
open /home/gitpod/.terraform.d/credentials.tfrc.json
```
Provide the following code (replace your token in the file)

```json
{
    "credentials": {
        "app.terraform.io": {
            "token": "Your-Terraform-Cloud-Token"
       }
   }       
}
```