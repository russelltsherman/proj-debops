# DebOps: Bootstrap hosts

DebOps bootstrap is an Ansible role that helps prepare a given Debian/Ubuntu host to be managed by Ansible.
It will install required Python packages, configure hostname and domain, create an admin account and set up SSH public keys for passwordless SSH access.

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
