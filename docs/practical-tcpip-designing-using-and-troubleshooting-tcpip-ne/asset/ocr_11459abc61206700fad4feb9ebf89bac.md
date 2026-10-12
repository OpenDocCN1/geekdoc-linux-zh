# 11.13 Troubleshooting (2) – a remote site can’t send to you

+   1. check your server logs. If the message wasn’t received, you need to find out if you’re receiving any mail at all. Your logs will tell you, but to be satisfyingly sure, logon to an external Web-based e-mail system like Hotmail, or a dial-up account, and send a short message to the end-user at your site who’s having the problem, and CC: the message to yourself at your own site too
+      – if you receive the Hotmail message, and especially if you are receiving mail for other sites, the problem may lie with the sender:
+        – see if you can send a message to them. To avoid any complications, do it manually using telnet to connect to their mail server
+        – ask them to send you another, short message, but before you do, run tcpdump to watch for any packets coming from their site. For example, if their mail server is 198.4.159.40, you could use
+          ```
+          tcpdump port 25 and host 198.4.159.40
+          ```
+          or if they have several servers use a "net" specification like
+          ```
+          tcpdump port 25 and net 198.4.159
+          ```
+          We’ve omitted "-n" because it will be easier to decipher the trace with names instead of numbers, and we’ve omitted "-t" because e-mail activity (as we saw in the mail headers in Module 11.8) can take minutes or hours, and you need to know at what time things happened.
+          If you don’t see any activity at all from their mail server(s), it looks even more like the problem is at their end. Ask them to send a test message to your Hotmail or other Web-mail account
+      – if you don’t receive the message you sent from Hotmail to your user and yourself, go to step 3 below.

+   2. if the logs show the message from the other site was received successfully but the user hasn’t retrieved it, check your POP server – see below.

+   3. you’re not receiving any mail. Check your SMTP server as you did in the previous module.

# Checking POP message retrieval

+   1. make sure the user’s client really is trying to retrieve messages. Run tcpdump to see what’s happening. For example, if the user’s PC is IP address 10.2.3.4, run
+      ```
+      tcpdump port 110 and host 10.2.3.4
+      ```

+   2. make sure the mail client has specified the correct POP server to retrieve from. You can check this manually but will also see it in the tcpdump trace

+   3. check that other people can retrieve messages: send yourself a short test message

+   4. try to retrieve the message manually as we showed in Module 11.10. If you can retrieve manually, the problem probably lies in this user’s client configuration, or this message