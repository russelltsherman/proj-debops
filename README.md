# infrastructure

This repo brings together a number of [tools](doc/TOOLS.md) to facilitate the definition of infrastructure as code.
It will facilitate automated provisioning of environments utiliing local baremetal, local virtual machines in VirtualBox as well as remote digital ocean droplets utilizing Terraform.

The intended purpose is to facilitate the provisioning and management of docker swarm hosts.

## Installing Prerequisites

See here for instructions for [installing prerequisites](doc/INSTALL.md)

## Local baremetal Provisioning using ansible

When your service hosts are local physical machines or remote machines whose base OS and networking setup has been completed.

See here for instructions for [baremetal provisioning](doc/BAREMETALPROVISION.md)

## Local virtual machine Provisioning using Vagrant

When your service hosts are local virtual machines.

See here for instructions for [vagrant provisioning](doc/VAGRANTPROVISION.md)

## Remote virtual machine Provisioning using Terraform

When your service hosts are remote virtual machines in Digital Ocean, AWS, Azure, or other cloud provider supported by Terrraform.

See here for instructions for [terraform provisioning](doc/TERRAFORMPROVISION.md)
