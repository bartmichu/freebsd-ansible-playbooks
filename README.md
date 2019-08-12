# FreeBSD Ansible Playbooks

Various ansible playbooks that I use to manage FreeBSD machines.

## Bootstrapping FreeBSD host

```shell
ansible -m raw -a "pkg install -y python" somebsdhost
```
