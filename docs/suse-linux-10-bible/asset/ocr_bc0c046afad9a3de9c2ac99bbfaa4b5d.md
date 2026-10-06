# Chapter 7 ♦ Logging 185

recommend you use RPM as opposed to the source distribution available unless you know what you are doing.

Listing 7-10 displays an example of mail sent to the root user by logcheck script. Note that under the heading Security Violations are two entries referring to failed login attempts via SSH.

# Listing 7-10: logcheck Example Mail

```
From root@bible.suse.com Thu May 27 23:23:41 2004
X-Original-To: root@bible.suse.com
Delivered-To:
Date: Thu, 27 May 2004 23:23:39 +0100
To: root@bible.suse.com
Subject: bible 05/27/04:23.23 system check
User-Agent: mail 10.6/15/03
MIME-Version: 1.0
Content-Type: text/plain; charset=us-ascii
Content-Transfer-Encoding: 7bit
From: root@bible.suse.com (root)
```

# Security Violations

```
--------------------------------------
May 27 23:23:35 sshd[5019]: error: PAM: Authentication failure
May 27 23:23:35 sshd[5019]: error: PAM: Authentication failure
```

# Unusual System Events

```
--------------------------------------
May 27 23:23:35 sshd[5019]: error: PAM: Authentication failure
May 27 23:23:35 sshd[5019]: error: PAM: Authentication failure
May 27 23:23:10 bible postfix/postfixlog[3881]: E47F918D21: uid=from=<root>
May 27 23:23:10 bible postfix/postfixlog[4941]: message-id=C0B666AB.mail13V42YZ@bible.suse.com E47F918D21:
May 27 23:23:11 bible postfix/postfixlog[3882]: from=<root@bible.suse.com>,\size=1261; ncpt=1 (queues active)
May 27 23:23:11 bible postfix/postfixlog[4941]: E47F918D21: to=<root@bible.suse.com>,
orig=<root>, relay=local, delay=1, status=delivered (delivered to mailbox)
May 27 23:23:11 bible postfix/postfixlog[3882]: E47F918D21: removed
```

How you set logcheck to run depends on how much data you receive in the email. If you have an active system, we recommend that you increase the frequency of the logcheck runs. If you have a relatively small system, running logcheck once a day will produce a manageable email that can be handled when things are quiet.