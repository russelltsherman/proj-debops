# VAGRANT: Provision local virtual machines

These instructions assume you've already installed and configured vagrant.
Please refer to the [documentation](VAGRANT.md) for more information on installation or configuration.

## Provision vagrant hosts

```bash
bin/vagrant up
```

See here for more instructions for [debops provisioning](DEBOPSPROVISION.md)

## destroy terraform hosts

```bash
bin/vagrant down
```

## Connect to a node to verify setup

```bash
vagrant ssh node01
```
