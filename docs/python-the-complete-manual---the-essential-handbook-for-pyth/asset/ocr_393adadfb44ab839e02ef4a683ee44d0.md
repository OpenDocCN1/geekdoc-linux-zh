# Python for system administrators Work with Python

+   - /dev/disk02 300G 175G 124G 59.0 / hfs / local
- devvs 191K 191K 0 - /dev devfs / none

+   - import base64, getpass, os, socket, sys,
socket, traceback
- import paramiko
- import interactive
- # setup logging
paramiko.util.log_to_file('demo_simple.log')
- # get hostname
username = ""
- if len(sys.argv) > 1:
hostname = sys.argv[1]
if hostname.find('@') >= 0:
username, hostname = hostname.

# Accessing Secure Shell (SSH) services

SSH (Secure Shell) is a modern replacement for old shell called Telnet. It allows data to be exchanged using a secure channel between two networked devices. Administrators frequently use SSH to administer networked systems. In addition to providing remote shell, SSH is also used for secure file transfer (using SSH File Protocol, or SFTP) and X server forwarding (allows SSH clients as X server). In this section we will learn how to use SSH using a Python module paramiko, which implements the SSH2 protocol for Python. paramiko can be installed using the following steps:

+   $ git clone https://github.com/robey/paramiko.git
- $ cd paramiko
- $ sudo setup.py install

```
split('@')
else:
hostname = raw_input('Hostname: ')
if len(hostname) == 0:
print('*** Hostname required.')
sys.exit(1)
port = 22
if hostname.find('::') >= 0:
hostname, portstr = hostname
split(':')
port = int(portstr)
```

To the core of paramiko is the SSHClient class. This class wraps L[Transport], L[Channel], and L[SFTPClient] to handle most of aspects of SSH. You can use SSHClient:

```
client = SSHClient()
client.load_system_host_keys()
client.connect('some.host.com')
stdin, stdout, stderr = client.exec_command('dir')
```

The following example demonstrates a full SSH client written using the paramiko module.

+   @code: PySSHClient

```
# get username
username = ""
default_username = getpass.getuser()
username = raw_input('Username [%s]: ' % (default_username))
if len(username) == 0:
default_password = getpass.getpass('Password for %s: ' % (default_username))
# now, connect and use paramiko Client to negotiate SSH2 across the connection
try:
```

```
client = paramiko.SSHClient()
client.load_system_host_keys()
client.set_missing_host_key_policy(paramiko.WarningPolicy)
```