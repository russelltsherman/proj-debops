# BAREMETAL: Provision local physical machines

These instructions assume you've already installed OS configured networking on barematal machines.
These instructions assume you've already installed modified the ansible inventory to include baremetal hosts.

## Provision hosts using ansible

ping our hosts to validate connectivity

```bash
ansible -m ping -u root -i ansible/inventory/hosts all
```

to limit DebOps command to only operate on terraform hosts add the -i flag to specify inventory file

```bash
debops bootstrap -i ansible/inventory/hosts --sudo -u root --ask-pass
debops common -i ansible/inventory/hosts -u devops
debops -i ansible/inventory/hosts
```

See here for more instructions for [debops provisioning](DEBOPSPROVISION.md)

## Connect to a node to verify setup

```bash
ssh root@<node-ip>
```
