# # Review Questions

+   1. Typing lsof -i | grep LISTEN as root produces three lines of output, corresponding to the sendmail, sshd, and proptpd servers. What can you conclude about the security of this system?

+   A. Everything's OK; the presence of sshd ensures that data are being encrypted by SSH. cure and should not be viewed.

+   B. The sendmail and sshd servers are OK, but the FTP protocol used by proptpd is insecure and should not be viewed.

+   C. The sendmail server should be replaced by postfix or qmail for improved security, sshd and proptpd are fine.

+   D. Because sendmail and proptpd both use unencrypted text-mode data, neither is appropriate on a network-connected computer.

+   E. No conclusion can be drawn without further information; the listed servers may or not be appropriate or authentic.

+   2. As part of a security audit, you plan to use Nmap to check all the computers on your network for unnecessary services. Which of the following tasks should you do prior to running your Nmap check?

+   A. Back up /etc/passwd on the target systems to eliminate the possibility of its being damaged.

+   B. Obtain the root passwords to the target servers so that you can properly configure them to accept the Nmap probes.

+   C. Obtain written permission from your boss to perform the Nmap sweep.

+   D. Configure /etc/sudoers on the computer you intend to use for the sweep, to give yourself the ability to run yourself.

+   E. Disable any firewall between the computer that's running Nmap and the servers you intend to scan.

+   3. Your login server is using PAM, and you want to limit users' access to system resources. Which configuration file will you need to edit?

+   A. /etc/pam/limits.conf

+   B. /etc/pam/limits.conf

+   C. /etc/security/limits.conf

+   D. /etc/security/pam/limits.conf

+   E. /usr/local/limits.conf

+   4. Which of the following tools might you use to check for open ports on a local computer? (Select three.)

+   A. Nmap

+   B. netstat

+   C. lsof

+   D. portmap

+   E. services