# infrastructure

This repo brings together a number of [tools](doc/TOOLS.md) to facilitate the definition of infrastructure as code.
It will facilitate both local definition of environments utilizing VirtualBox as well as remote definition of environments utilizing Terraform.

The intended purpose is to facilitate the provisioning and management of docker swarm hosts.

## Required Prerequisites

See here for instructions for [installing prerequisites](doc/INSTALL.md)

## Provision local virtual machines

Initialize VirtualBox virtual machines as defined in VagrantMachines.yml

```bash
vagrant up
```

## Bootstrap local virtual machines

DebOps bootstrap is an Ansible role that helps prepare a given Debian/Ubuntu host to be managed by Ansible. It will install required Python packages, configure hostname and domain, create an admin account and set up SSH public keys for passwordless SSH access.

```bash
debops bootstrap --sudo -u vagrant --ask-pass
```

provide the password `vagrant` when prompted

## DebOps secrets

An optional step that allows you to encrypt your ansible secrets directory using EncFS and GPG.

```bash
debops-padlock init
```

## Run DebOps common playbook on all hosts

Apply a number of DebOps common roles to provide baseline function see [here](https://github.com/debops/debops-playbooks/blob/master/playbooks/common.yml) for details.

```bash
debops common -u devops
```

## Run Custom site playbook on all hosts

Apply our custom roles see [here](ansible/playbooks) for details

```bash
debops
```

## Connect to a node to verify setup

```bash
vagrant ssh node01
```
