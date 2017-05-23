# TERRAFORM: Provision remote virtual machines

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
