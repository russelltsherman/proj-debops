# VAGRANT: Provision local virtual machines

Initialize VirtualBox virtual machines as defined in VagrantMachines.yml

```bash
vagrant up
```

## Provision hosts using ansible

See here for instructions for [debops provisioning](DEBOPSPROVISION.md)

to limit DebOps command to only operate on vagrant hosts add the -i flag to specify inventory file

```bash
debops -i ansible/inventory/hosts_vagrant
```

## Connect to a node to verify setup

```bash
vagrant ssh node01
```
