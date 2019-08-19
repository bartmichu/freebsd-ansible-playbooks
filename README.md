# FreeBSD Ansible Playbooks

Various ansible playbooks that I use to manage FreeBSD machines.

## freebsd-packages-upgrade.yaml

This is a playbook to upgrade all installed packages on FreeBSD hosts.
It will explicitly update local repository catalogue before upgrading packages and then show a list of upgraded packages at the end.

Sample output with debugging turned off:

```shell
$ ansible-playbook --ask-become-pass freebsd-packages-upgrade.yaml
BECOME password:

PLAY [Upgrade installed packages on FreeBSD hosts] *****************************

TASK [Gathering Facts] *********************************************************
ok: [freebsd-ansible]

TASK [Explicitly update local repository catalogue] ****************************
changed: [freebsd-ansible]

TASK [Upgrade packages] ********************************************************
changed: [freebsd-ansible]

TASK [Show a list of upgraded packages] ****************************************
ok: [freebsd-ansible] => {
    "msg": [
        "[1/2] Upgrading nginx from 1.16.0_2,2 to 1.16.1_2,2...", 
        "[2/2] Upgrading libnghttp2 from 1.39.1_1 to 1.39.2..."
    ]
}

PLAY RECAP *********************************************************************
freebsd-ansible            : ok=4    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

## freebsd-system-update.yaml

This is a playbook to fetch and install binary system updates on FreeBSD hosts. If any updates are installed then it will also show a summary with old/new system version and patch level.

Sample output with debugging turned off:

```shell
$ ansible-playbook --ask-become-pass freebsd-system-update.yaml
BECOME password:

PLAY [Fetch and install binary system updates on FreeBSD hosts] ****************

TASK [Gathering Facts] *********************************************************
ok: [freebsd-ansible]

TASK [Fetch binary system updates] *********************************************
changed: [freebsd-ansible]

TASK [Install recently fetched binary system updates] **************************
changed: [freebsd-ansible]

TASK [Get new system version and patch level] **********************************
changed: [freebsd-ansible]

TASK [Show update summary] *****************************************************
ok: [freebsd-ansible] => {
    "msg": "System updated from 12.0-RELEASE-p6 to 12.0-RELEASE-p9"
}

PLAY RECAP *********************************************************************
freebsd-ansible            : ok=5    changed=3    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

## Bootstrapping a FreeBSD host

```shell
ansible -m raw -a "pkg install -y python" somebsdhost
```
