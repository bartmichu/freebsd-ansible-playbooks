# FreeBSD Ansible Playbooks

Various ansible playbooks that I use to manage FreeBSD machines.

## freebsd-packages-upgrade.yaml

This is a playbook to upgrade all installed packages on FreeBSD hosts.
It will explicitly update local repository catalogue before upgrading packages and then show a list of upgraded packages at the end. Optionally (False by default) it can also create a new Boot Environment before upgrading packages.

Sample output:

```shell
ansible-playbook -l test_freebsd -K freebsd-packages-upgrade.yaml
BECOME password:

PLAY [Upgrade installed packages on FreeBSD hosts] *****************************

TASK [Gathering Facts] *********************************************************
ok: [freebsd-ansible]

TASK [Explicitly update local repository catalogue] ****************************
changed: [freebsd-ansible]

TASK [Check for outdated packages] *********************************************
changed: [freebsd-ansible]

TASK [Check if Boot Environments are supported] ********************************
skipping: [freebsd-ansible]

TASK [Create a new Boot Environment] *******************************************
skipping: [freebsd-ansible]

TASK [Upgrade installed packages] **********************************************
changed: [freebsd-ansible]

TASK [Show a list of upgraded packages] ****************************************
ok: [freebsd-ansible] => {
    "msg": [
        "[1/4] Upgrading nginx from 1.16.0_2,2 to 1.16.1_2,2...", 
        "[2/4] Upgrading nano from 4.3 to 4.4...", 
        "[3/4] Upgrading libnghttp2 from 1.39.1_1 to 1.39.2...", 
        "[4/4] Upgrading ca_root_nss from 3.45 to 3.46..."
    ]
}

PLAY RECAP *********************************************************************
freebsd-ansible            : ok=5    changed=3    unreachable=0    failed=0    skipped=2    rescued=0    ignored=0
```

## freebsd-system-update.yaml

This is a playbook to fetch and install binary system updates on FreeBSD hosts. Optionally (True by default) it can create a new boot environment before installing updates on ZFS systems. If any updates are installed then it will also show a summary with old/new system version and patch level. Works with ZFS and UFS based installations.

Sample output:

```shell
$ ansible-playbook --ask-become-pass freebsd-system-update.yaml
BECOME password:

PLAY [Fetch and install binary system updates on FreeBSD hosts] ****************

TASK [Gathering Facts] *********************************************************
ok: [freebsd-ansible]

TASK [Fetch binary system updates] *********************************************
changed: [freebsd-ansible]

TASK [Check if Boot Environments are supported] ********************************
changed: [freebsd-ansible]

TASK [Create a new Boot Environment] *******************************************
changed: [freebsd-ansible]

TASK [Install recently fetched binary system updates] **************************
changed: [freebsd-ansible]

TASK [Get new system version and patch level] **********************************
changed: [freebsd-ansible]

TASK [Show update summary] *****************************************************
ok: [freebsd-ansible] => {
    "msg": "System updated from 12.0-RELEASE-p9 to 12.0-RELEASE-p10"
}

PLAY RECAP *********************************************************************
freebsd-ansible            : ok=7    changed=5    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

## Bootstrapping a FreeBSD host

```shell
ansible -m raw -a "pkg install -y python" somebsdhost
```
