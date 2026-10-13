+   - Simply sign an agreement with MAPS RBL, transfer the entire database onto a local host, and create a local RBL for your own use.
+   - Query the master RBL database on a case-by-case basis.

The latest version of sendmail (8.9.x) comes with RBL. The Red Hat Linux RPM available for the latest version enables RBL in /etc/sendmail.cf, so you do not have to do anything to configure it. Here is how you test the RBL configuration in your sendmail.

+   1. Run the following:
+   ```
+   sendmail -bt
+   ```
+   2. At the address test mode prompt, enter:
+   ```
+   .D{client_addr}127.0.0.1
+   Basic_check_relay <>
+   ```
+   The output looks like the following:
+   ```
+   ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
+   Enter <ruleset> <address>
+   > .D{client_addr}127.0.0.1
+   > Basic_check_relay <>
+   rewrite: ruleset 190 input: < >
+   rewrite: ruleset 190 returns: OKSO FAR
+   ```
+   This tells you that the address 127.0.0.1 (loopback address) is not blocked in RBL, because the rewrite result was OKSO FAR.
+   3. Now, duplicate the preceding test using 127.0.0.2 (the RBL-supplied test IP, which is blocked in RBL). You should see output similar to the following:
+   ```
+   ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
+   Enter <ruleset> <address>
+   > .D{client_addr}127.0.0.2
+   > Basic_check_relay <>
+   rewrite: ruleset 190 input: < >
+   ```