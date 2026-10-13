
```
[@student deploy-review]$ ansible all -m copy \
- a 'content=This server is managed by Ansible.\n' dest="/etc/motd" --become
server.lab.com | CHANGED => {
"ansible_facts": {
  "discovered_interpreter_python": "/usr/libexec/platform-python",
  "changed": true,
  "checksum": "93d034884285bb267952b95e0180667effc69ad",
  "dest": "/etc/motd",
  "gid": "0",
  "group": "root",
  "md5sum": "a7f4293c7b2a738c4f870644374e94177a",
  "mode": "0644",
  "owner": "root",
  "size": "35",
  "src": "/home/devops/.ansible/tmp-155895417.7240693-24998294084061/",
  "state": "file",
  "uid": "0"
}
nserver.lab.com | CHANGED => {
"ansible_facts": {
  "discovered_interpreter_python": "/usr/libexec/platform-python"
,
  "changed": true,
  "checksum": "93d30448245bb2679572b95e0180607eff69ad",
  "dest": "/etc/motd",
  "gid": "0",
  "group": "root",
  "md5sum": "af74293c7b2a738c4f870644374e94177a",
  "mode": "0644",
  "owner": "root",
  "secontext": "system_u:object_r:etc_t:s0",
  "size": "35",
  "src": "/home/devops/.ansible/tmp-155895417.7165847-19332401382206",
  "state": "file",
  "uid": 0
}
serverlab.example.com | CHANGED => {
"ansible_facts": {
  "discovered_interpreter_python": "/usr/libexec/platform-python"
},
  "changed": true,
  "checksum": "93d30448245bb2679572b95e0180667ad",
  "dest": "/etc/motd",
  "gid": "0",
  "group": "root",
  "md5sum": "af74293c7b2a738c4f870644374e94177a",
  "mode": "0644",
  "owner": "root",
  "secontext": "system_u:object_r:etc_t:s0",
  "size": "35",
  "src": "/home/devops/.ansible/tmp-155895417.75727-9415172230122",
  "state": "file",
  "uid": 0
}
serverlab.example.com | CHANGED => {
"ansible_facts": {
  "discovered_interpreter_python": "/usr/libexec/platform-python"
},
  "changed": true,
  "checksum": "93d30448245bb2679572b95e0180667ad",
  "dest": "/etc/motd",
  "gid": "0",
  "group": "root",
  "md5sum": "af74293c7b2a738c4f870644374e94177a",
  "mode": "0644",
  "owner": "root",
  "secontext": "system_u:object_r:etc_t:s0",
  "size": "35",
  "src": "/home/devops/.ansible/tmp-155895417.6649802-531238237104",
  "state": "file",
  "uid": 0
}
```

7. 如果你再次运行即性命令，你应该看到 `copy` 模块检测到文件是正确的且没有更改。寻找即性命令报告 `SUCCESS` 以及每个托管主机的 `"changed": false`。

```
[student@workstation deploy-review]$ ansible all -m copy \
- a 'content=This server is managed by Ansible.\n' dest="/etc/motd" --become serverb.lab.example.com | SUCCESS => {
  "ansible_facts": {
  "discovered_interpreter_python": "/usr/libexec/platform-python",
    "changed": false,
    "checksum": "93d304488254bb267952b95e0180667ad",
    "dest": "/etc/motd",
    "gid": 0,
    "group": "root",
    "mode": "0644",
    "owner": "root",
    "path": "/etc/motd",
    "secontext": "system_u:object_r:etc_t:s0",
    "size": 35,
    "state": "file",
    "uid": 0
  }
serverb.lab.example.com | SUCCESS => {
  "ansible_facts": {
    "discovered_interpreter_python": "/usr/libexec/platform-python",
    "changed": false,
    "checksum": "93d304488254bb267952b95e0180667ad",
    "dest": "/etc/motd",
    "gid": 0,
    "group": "root",
    "mode": "0644",
    "owner": "root",
    "path": "/etc/motd",
    "secontext": "system_u:object_r:etc_t:s0",
    "size": 35,
    "state": "file",
    "uid": 0
  }
serverb.lab.example.com | SUCCESS => {
  "ansible_facts": {
    "discovered_interpreter_python": "/usr/libexec/platform-python",
    "changed": false,
    "checksum": "93d304488254bb267952b95e0180667ad",
    "dest": "/etc/motd",
    "gid": 0,
    "group": "root",
    "mode": "0644",
    "owner": "root",
    "path": "/etc/motd",
    "secontext": "system_u:object_r:etc_t:s0",
    "size": 35,
    "state": "file",
    "uid": 0
  }
}
```
