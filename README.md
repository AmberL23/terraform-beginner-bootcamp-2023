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

### AWS CLI Installation

AWS CLI is installed for the project via the bash script [`./bin/install_aws_cli`](./bin/install_aws_cli)

[Getting Started Install (AWS CLI)](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)

[AWS CLI Env Vars](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-envvars.html)

We can check if your AWS credentials are configured correctly by running the following AWS CLI command:

```sh
aws sts get-caller-identity
```   
If it is successful you should see a json payload return that looks like this"

```json

    "UserId": "AIDA4G6BXYYD2URT870SX3",
    "Account": "123123123123",
    "Arn": "arn:aws:iam::123123123123:user/terraform-beginner-bootcamp"```

We will need to generate AWS CLI credentials from IAM user in order to us the aws CLI


