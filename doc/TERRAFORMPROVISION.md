# TERRAFORM

These instructions assume you've already installed and configured Terraform.
Please refer to the [documentation](TERRAFORM.md) for more information on installation or configuration.

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

ping our hosts to validate connectivity

```bash
ansible -m ping -u root -i ansible/inventory/hosts_terraform all
```

to limit DebOps command to only operate on terraform hosts add the -i flag to specify inventory file

```bash
debops bootstrap -i ansible/inventory/hosts_terraform
debops common -i ansible/inventory/hosts_terraform -u devops
debops -i ansible/inventory/hosts_terraform
```

See here for more instructions for [debops provisioning](DEBOPSPROVISION.md)

## Connect to a node to verify setup

```bash
ssh root@<node-ip>
```
