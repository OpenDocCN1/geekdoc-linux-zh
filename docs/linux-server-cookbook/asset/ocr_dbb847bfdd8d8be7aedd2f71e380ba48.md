```
ansible_connection: winrm
ansible_host: 192.168.122.33
```

An inventory can contain a range of hosts; the following example will define five Web servers in one line:

```
web0[1:5].example.com
```

# AD-HOC actions

Ansible brings the command ansible to check connectivity to the nodes or to perform simple tasks. This task is not saved in any file and does not need any file to read the task to be performed. The syntax is as follows:

```
ansible [options] servers|groups|all|ungrouped -m module [-a arguments]
```

The module used to check connectivity is named ping. If the connectivity is correct, it will show the word "pong", and the task will be marked as SUCCESS. If the connection fails, it will be marked as UNREACHABLE. Figure 12.17 shows the two scenarios:

```
agonzalez@ubuntu:~$ ansible -i /etc/ansible/hosts -m ping rhel
rhel | SUCCESS => {
  "ansible_facts": {
    "discovered_interpreter_python": "/usr/bin/python3"
  },
  "changed": false,
  "ping": "pong"
}
agonzalez@ubuntu:~$ ansible -i /etc/ansible/hosts -m ping web01.example.com
web01.example.com | UNREACHABLE! => {
  "changed": false,
  "msg": "Failed to connect to the host via ssh: ssh: Could not resolve host name web01.example.com: Temporary failure in name resolution",
  "unreachable": true
}
```

![](bbox=[0.3, 0.74, 0.7, 0.77])

Other common modules to be used in the ad-hoc mode are as follows:

+   - command: Execute a command in the managed nodes.
+   - shell: Execute a command in the managed node but using the shell configuration.