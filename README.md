# FreeBSD Ansible Playbooks

Various ansible playbooks that I use to manage FreeBSD machines.

## freebsd-packages-upgrade.yaml

This is a playbook to upgrade packages on FreeBSD hosts.

## freebsd-system-update.yaml

This is a playbook to fetch and install binary system updates on FreeBSD hosts.

## Bootstrapping FreeBSD host

```shell
ansible -m raw -a "pkg install -y python" somebsdhost
```
