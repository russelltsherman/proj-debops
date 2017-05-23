# TERRAFORM

This project currently assumes that you are provisioning hosts using Digital Ocean.

Before moving forward log into your Digital Ocean account and generate an API token.

## Configure terraform

copy `terraform.tfvars.example` to `terraform.tfvars`

edit `terraform.tfvars` and paste your Digital Ocean API token

[create an SSH public key](https://confluence.atlassian.com/bitbucketserver/creating-ssh-keys-776639788.html) if you do not already have one.

execute `bin/do_ssh_key` to send your ssh publick key to your digital ocean account.  This will write your SSH key fingerprint to `terraform.tfvars` for later use.

## Provision remote virtual machines

Generate terraform plan file

```bash
terraform plan -out terraform.plan
```

Apply terraform plan

```bash
terraform apply terraform.plan
```

Read terraform state and write ansible/inventory/hosts_terraform

```bash
bin/do_tf_inventory
```

## Provision hosts using ansible

See here for instructions for [debops provisioning](DEBOPSPROVISION.md)

to limit DebOps command to only operate on terraform hosts add the -i flag to specify inventory file

```bash
debops -i ansible/inventory/hosts_terraform
```

## Connect to a node to verify setup

```bash
ssh root@<node-ip>
```
