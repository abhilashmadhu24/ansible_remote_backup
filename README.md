Hi,

This is a simple ansible playbook for enabling backups on multiple remote servers which doesn't have a centralised backup system available 
like managed cloud providers. This playbook will help to enable important file backups on multiple  on-premis/unmanaged data-center servers.

PL: I have used a sample file backup bash script for taking backups as this is a demo only. You can replace it with your requirements.

Pre-requisites: Ubuntu 18.04 + Ansible 2.6 on master server Ubuntu 18.04 on remote servers with ssh key authentication



Steps on master server:
```
>> apt get install ansible
>> git clone https://github.com/abhilashmadhu24/ansible_remote_backup.git
>> cd ansible_remote_backup
>> Edit inventory file and put remote server's details 
>> Edit or replace files/backup.sh.j2 with your own script 
>> ansible-playbook host.yml
```

For changing cron timings , edit backup.yml and change as per your requirements

Output should look like

```
root@server:# ansible-playbook backup.yml 

PLAY [remote] *******************************************************************************************

TASK [Gathering Facts] **********************************************************************************
ok: [172.16.2.223]
ok: [172.16.5.228]
ok: [172.16.5.175]
ok: [172.16.5.10]
ok: [172.16.5.143]

TASK [Install prerequisites] *****************************************************************************
ok: [172.16.2.223] => (item=python)
ok: [172.16.5.175] => (item=python)
ok: [172.16.5.10] => (item=python)
ok: [172.16.5.228] => (item=python)
ok: [172.16.5.143] => (item=python)

TASK [Creating remote folders] ***************************************************************************
ok: [172.16.2.223]
ok: [172.16.5.143]
ok: [172.16.5.228]
ok: [172.16.5.10]
ok: [172.16.5.175]

TASK [Sending backup shell script to remote locations] ***************************************************
ok: [172.16.2.223]
ok: [172.16.5.143]
ok: [172.16.5.228]
ok: [172.16.5.10]
ok: [172.16.5.175]

TASK [Creating backup-cron jobs on daily basis on remote locations] **************************************
ok: [172.16.5.175]
ok: [172.16.2.223]
ok: [172.16.5.228]
ok: [172.16.5.143]
ok: [172.16.5.10]

PLAY RECAP ***********************************************************************************************
172.16.2.223               : ok=5    changed=0    unreachable=0    failed=0   
172.16.5.10                : ok=5    changed=0    unreachable=0    failed=0   
172.16.5.143               : ok=5    changed=0    unreachable=0    failed=0   
172.16.5.175               : ok=5    changed=0    unreachable=0    failed=0   
172.16.5.228               : ok=5    changed=0    unreachable=0    failed=0

```
