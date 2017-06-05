# BAREMETAL: Provision local physical machines

These instructions assume you've already installed OS configured networking on barematal machines.
These instructions assume you've already installed modified the ansible inventory to include baremetal hosts.

## Provision baremetal hosts

```bash
bin/baremetal up
```

See here for more instructions for [debops provisioning](DEBOPSPROVISION.md)

## Connect to a node to verify setup

```bash
ssh root@<node-ip>
```
