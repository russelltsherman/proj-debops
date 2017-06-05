# TERRAFORM

These instructions assume you've already installed and configured Terraform.
Please refer to the [documentation](TERRAFORM.md) for more information on installation or configuration.

## Provision terraform hosts

```bash
bin/terraform up
```

See here for more instructions for [debops provisioning](DEBOPSPROVISION.md)

## destroy terraform hosts

```bash
bin/terraform down
```

## Connect to a node to verify setup

```bash
ssh root@<node-ip>
```
