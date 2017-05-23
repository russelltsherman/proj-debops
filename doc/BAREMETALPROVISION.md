# BAREMETAL: Provision local physical machines

These instructions assume you've already installed OS configured networking on barematal machines.
These instructions assume you've already installed modified the ansible inventory to include baremetal hosts.

## Provision hosts using ansible

See here for instructions for [debops provisioning](DEBOPSPROVISION.md)

to limit DebOps command to only operate on terraform hosts add the -i flag to specify inventory file

```bash
debops -i ansible/inventory/hosts
```

## Connect to a node to verify setup

```bash
ssh root@<node-ip>
```
