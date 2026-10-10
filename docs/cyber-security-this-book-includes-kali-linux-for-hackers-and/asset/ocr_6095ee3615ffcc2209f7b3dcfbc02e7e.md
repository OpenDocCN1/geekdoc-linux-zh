The demonstrations presented below allow strengthening the use of some tools presented during the Course. These demonstrations focus on the Exploitation and Post-Exploitation phase, that is, the processes that an attacker would perform after gaining access to the system by exploiting a vulnerability.

Demonstration using a local exploit to escalate privileges.
# ssh -l msfadmin 192.168.159.129
Once inside the system we proceed to use the "sudo" command.
# sudo cat /etc/shadow
# sudo passwd root

Enter a new password and then
# your root
# id

The Post Exploitation phase would be similar to the one detailed in the first example.