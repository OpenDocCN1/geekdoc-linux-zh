ansible_ssh_common_args | Specifies the arguments to be used for SSH.

Table 12.4: Ansible variables on the inventory

Ansible auto generates two groups automatically:

+   - all: It includes all the hosts defined in the inventory.
+   - ungrouped: It includes all the hosts which do not belong to any group.

It is also possible to define groups containing another group, as is shown in the following example:

```
anoherost ansible_host=192.168.122.44
[production:children]
linux
windows
[linux]
rhel ansible_host=192.168.122.43
ubuntu ansible_host=192.168.122.226
[windows]
win01 ansible_host=192.168.122.33 ansible_connection=winrm
```

In the previous example, the group production will contain three hosts: rhel, ubuntu, and win01. The node anotherhost will be part of the groups ungrouped and all. Ansible provides a command named ansible-inventory to query the inventory indicated to display the configured inventory. Figure 12.15 shows an example with the option --graph:

```
agonzalez@ubuntu:~$ ansible-inventory  -i /etc/ansible/hosts --graph
@all:
|--@production:
|  |--@linux:
|  |   |--rhel
|  |   |--ubuntu
|  |--@windows:
|     |--win01
|--@ungrouped:
|  |--anotherhost
```

Figure 12.15: Output example for command ansible-inventory