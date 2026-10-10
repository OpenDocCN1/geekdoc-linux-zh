command and a set of numbers to set the permission of the file. “chmod 777 test.sh” makes the file readable, writable, and executable by all users anywhere because each specification (owner, group, other) has the number 7 attached to it. Numbers determine the permissions that entity has, and the number used is calculated like so:

+   *   Start with the number 0.
+   *   Add 4 for adding readability.
+   *   Add 2 for write-ability.
+   *   Add 1 for executable-ness.
+   *   The number you have left determines the permissions.

6 would be read/write, but 1 would only be executable. 5 would be readable and executable, but not changeable. In our 777 example, we set owner, group, and others to all be 7. This is not particularly good security, because that means anybody anywhere can mess with that file. A more conservative permission set would be 775. Use security permissions advantageously for secure computing.

Security within Linux expands beyond just permissions. Ensure that you practice good security practices, and that you are following common sense in regards to security- install only needed programs, do not follow all internet advice, do not use sudo too often, use passwords, use encrypted networks, keep software up to date, encrypt important files, and make regular backups. As a final word