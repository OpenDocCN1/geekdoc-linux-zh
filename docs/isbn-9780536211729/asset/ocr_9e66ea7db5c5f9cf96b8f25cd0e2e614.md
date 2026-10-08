of “easy” paths that could be made “hard” to do with minimal effort. To increase security, analyze the difficulty of each path segment and to either eliminate easy paths or make them harder.

> The use of attack paths is a part of failure analysis, the science of analyzing possible failure modes of the system. It is helpful, regardless of whether the system is a computer, bridge, airplane, or space ship and is used by engineers designing all of these.

Recognize too that it is impossible to find all the paths, even for experts with decades of experience. The attack paths method is but one tool for increasing system security.

Some ways to harden this system are:

+   1. Use shadow passwords to prevent a cracker from getting the encrypted password so she can crack it on own system. We “Shadowed MD5 Passwords for Good Security” on page 41 for details on implementing shadow passwords.
2. Configure FTP to run chroot so it cannot get at /etc/passwd or /tmp. Most recent distributions as shipped already operate this way. Use the chroot capability for other daemons too, such as named.
3. Do not allow root’s$PATH to contain ".
4. Disable all unnecessary services, such as the finger daemon.
5. Do not put users’ account names (e-mail addresses) on the Web site.
6. Ensure hard-to-crack passwords. We “Passwords—A Key Point for Good Security” on page 35.
7. Ensure that there is no buggy set-UID programs. Keep software upgraded to latest versions. Have programs set-UID to accounts other than root wherever possible. Find alternatives to set-UID programs (where this would increase security).
8. Hire a good consultant to audit your security and perform penetration testing.

Attack paths can be a tremendous help in analyzing for security problems. This is particularly true for locally added applications, including CGI programs. Because CGIs commonly harbor security holes (bugs) this will allow you to determine how serious the consequences might be. This technique also will help you see how different variations limit the damage done if a vulnerability is discovered in a CGI (or other application). It will allow you to see which CGIs are most critical from a security perspective and which ones one should get the most detailed security analysis.