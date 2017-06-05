# Terraform

- Terraform is a tool for building, changing, and versioning infrastructure safely and efficiently. Terraform can manage existing and popular service providers as well as custom in-house solutions.

## Install Terraform

Download and install Terraform either [from the website](https://www.terraform.io/downloads.html) or use homebrew.

`brew install terraform`

Install python requirements for our terraform helper scripts

```bash
pip install -r requirements.txt
```

## Configuration Files

- **Terraform.tf**: This file is used by Terraform to spin up the remote cloud machines.

- **.vars.example**: Copy this file to `.vars` and place your Digital Ocean API token inside

## Upload your SSH key to Digital Ocean

This script will upload your ssh key to digital ocean and write it's fingerprint to `.vars`

```bash
bin/do_ssh_key ~/.ssh/id_rsa.pub
```

Load the content of the updated `.vars` file into your shell
```bash
source .vars
```

## Instructions

These instructions assume you've already installed Terraform.
Please see above for more information on installation or configuration.

1. Use `terraform plan` to view changes required to bring providers up to current state

1. Use `terraform plan -out terraform.plan` to write a plan file to the given path. This can be used as input to the "apply" command.

1. User `terraform plan -destroy -out terraform.plan` to create a plan file to revert droplets

1. Use `terraform apply terraform.plan` to apply the plan file at the given path.
