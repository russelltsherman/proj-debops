# DebOps

YOUR DEBIAN-BASED DATA CENTER IN A BOX

A collection of Ansible playbooks, scalable from one container to an entire data center.

## Install DebOps

DebOps scripts are distributed on PyPI, Python Package Index. They can be installed using the pip command:

`pip install debops`

You can also use pip to upgrade the scripts themselves:

`pip install --upgrade debops`

After the installation is finished, scripts will be available in `/usr/local/bin/`, which should be in your shell's `$PATH`.

## DebOps prerequisites

To use DebOps playbooks, you need some additional tools on your Ansible Controller besides the official scripts.

- uuidgen

This command is used to generate unique identifiers for hosts which are then saved as Ansible facts and can be used to identify hosts in the playbook. In most Linux or MacOSX desktop distributions this command should be already installed. If not, it can be usually found in the uuid-runtime package.

- encfs

This is an optional application, which is used by the debops-padlock script to encrypt the secret/ directory within DebOps project directories, which holds confidential data like passwords, private keys and certificates. EncFS is available on Linux distributions, usually as the encfs package.

`brew cask install osxfuse`
`brew install encfs`

- gpg

GnuPG is used to encrypt the file which holds EncFS password; this allows you to share the encrypted secret/ directory with other users without sharing the password, and using private GPG keys instead. debops script will automatically decrypt the keyfile and use it to open an EncFS volume. GnuPG is usually installed on Linux or MacOSX operating systems.

`brew install gnupg`

- git

Git is required to be installed for Debops to be used. Git is a version control system. If it is not already installed, it can be usually be installed using your favourite package manager.

## Instructions

These instructions assume you've already installed DebOps and any necessary prerequisites. Please refer to the documentation for those products for more information on installation or configuration.

1. Use `debops-update` to pull latest versions of DebOps roles and playbooks

## Manually running DebOps

debops playbooks should be applied to hosts using Vagrant or Terraform the following commands are just FYI.

### bootstrap hosts

run the debops bootstrap playbook on each host to add our admin user and our ssh key

`debops bootstrap -l <hostname> --sudo -u <username> --ask-pass`

### apply debops common playbook

now we will run the debops common playbook to do some additional configuration

`debops common -u <username>`

### run debops

now we will run the debops site playbook to configure all hosts and services

`debops`
