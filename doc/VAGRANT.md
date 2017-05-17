# Vagrant

- Vagrant is a tool for building and managing local virtual machine environments

## Install Vagrant

Download and install Vagrant either [from the website](https://www.vagrantup.com/downloads.html) or use homebrew.

`brew cask install vagrant`

## Files

- **Vagrantfile**: This file is used by Vagrant to spin up the virtual machines. You should be able to use this file unchanged; all the VM configuration options are stored in `VagrantMachines.yml`

- **VagrantMachines.yml**: This YAML file contains a list of VM definitions and associated configuration data. It is referenced by `Vagrantfile` when Vagrant instantiates the VMs.

## Instructions

These instructions assume you've already installed Vagrant, the necessary back-end virtualization provider(s) (only VirtualBox is supported by this testing environment), and any necessary plugins. Please refer to the documentation for those products for more information on installation or configuration.

1. Use `vagrant box add` to add a VirtualBox box and/or a VMware Fusion box (any box marked with "vmware_desktop" provider will work with Fusion). If you have both VMware Fusion and VirtualBox installed on the same system, install a box for both platforms.

1. Edit the `VagrantMachines.yml` file to ensure the box(es) you downloaded in step 1 is/are specified in this file. Place the name of the VirtualBox box as the value for "vb_box"; supply the name of the VMware Fusion box as the value for "vmw_box".

1. Run `vagrant up`. Vagrant will create the VM using the box specified in `VagrantMachines.yml`, selecting the appropriate box based on the provider in use.

1. Run `vagrant ssh <machine-name>` to connect to the host via ssh console use password `vagrant` when prompted.
