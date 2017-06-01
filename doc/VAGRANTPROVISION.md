# VAGRANT: Provision local virtual machines

Initialize VirtualBox virtual machines as defined in VagrantMachines.yml

```bash
vagrant up
```

## Provision hosts using ansible

ping our hosts to validate connectivity

```bash
ansible -m ping -u root -i ansible/inventory/hosts_vagrant all
```

to limit DebOps command to only operate on vagrant hosts add the -i flag to specify inventory file

```bash
debops bootstrap -i ansible/inventory/hosts_vagrant --sudo -u vagrant --ask-pass
debops common -i ansible/inventory/hosts_vagrant -u devops
debops -i ansible/inventory/hosts_vagrant
```

See here for more instructions for [debops provisioning](DEBOPSPROVISION.md)

## Connect to a node to verify setup

```bash
vagrant ssh node01
```
