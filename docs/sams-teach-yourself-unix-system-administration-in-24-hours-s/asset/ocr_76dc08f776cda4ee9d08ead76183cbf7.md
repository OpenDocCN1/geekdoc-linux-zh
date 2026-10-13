# Workshop

# Quiz

+   1. What’s the main reason for updating your version of BIND?
+   2. What happens if you omit the trailing dots on domain names in the ORIGIN section of a zone file?
+   3. What would happen if a TTL for a master record was set to 60? Would that be good or bad?
+   4. What should you always remember to do when you edit a zone file?
+   5. Why is it dangerous to let other hosts update your zone configuration files through rndc?
+   6. What very important thing happens if you use the command rndc stop that doesn’t occur with rndc halt?

# Answers

+   1. In a word: security.
+   2. ORIGIN names that lack a trailing dot have the hostname automatically prefaced, changing the intent of the statement in the zone file in most cases.
+   3. Setting the TTL too low will cause the network to saturate, as DNS caches keep asking for new authoritative records again and again. It’d definitely be bad.
+   4. Update or increment the serial number in the zone file.
+   5. See Answer #1.
+   6. The stop command saves any changes to the zone information by rewriting the master files. The halt command does not change the master files.

A name server is a single Internet service, as is a Web server (covered in the last two hours of this book). The next hour will focus on a variety of different Internet services, including a discussion of how to enable or disable ftp access, and an exploration of the useful telnet utility.