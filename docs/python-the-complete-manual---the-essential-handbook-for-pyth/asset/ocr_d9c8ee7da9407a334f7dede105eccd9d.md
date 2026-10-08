# Sending email

# Introducing Python

40 You can use the module
smtplib to send an
SMTP (Simple Mail Transfer Protocol)
client interface.

```
FTP(host,username,password)
# Download the file
uu = urllib2.urlopen("ftp://
ftp.redhat.com/pub/redhat/
/README")
# Print the file contents
print(u.read())
```

smtplib(SMTP, [port])
Example send an email using
Google SMTP server:

```
import smtplib
# Use your own to from
email address
fromaddr = 'kunaldo@gmail.com'
toaddr = 'to@gmail.com'
msg = 'I am a Python geek.'
Here is the proof!'
```

+   # Credentials
# Use your Google Mail
credentials while running the
program

```
username = 'kunaldo@gmail.com'
password = 'password'
# The actual mail
server = smtplib.SMTP('smtp.
gmail.com:587')
# Google Mail uses secure
connection for SMTP
server.starttls()
server.login(username,password)
server.sendmail(fromaddr,
toaddr,msg)
server.quit()
```

```
30d1e7f41000b220448a42f9f0e5b7c7/
7a9b4890aa835e5c2/
# sha256 Digest
>> sha256:a616(Classified
Information (007))
2fd6c73d77a4767f2db397299169
b2590066f4e0e33b11852e5/
>> sha384:338a6(Classified
Information (007))
5a9141f003d9141d4edc70a488b69
9ec82d13ac7286998a4d4f50e6
9e0f5c1c356563b757d4/
# sha512 Digest
>> sha512:a6616(Classified
Information (007))
7a0c33dfe8f5e234872a8255d5d5d5
```

# Launching a web server
with web browser

Older versions of Red Hat Linux
have moved to the following location:
archive.redhat.com/
pub/redhat/linux/

```
[-/usr/python] ftplib
```

The 'webmaster' module
provides a convenient way to
lauch using the default

Example (google.co.uk
with system's default web
browser):

```
>> import urllib
>> webdriver.open("http://
localhost:8000")
True
```

# Creating hashes

The 'hashmaster' module
support a plethora of
secure hash algorithms including
SHA1, SHA256, SHA384,
SHA512 and MD5.

Example hex digest of
the given text:

```
>> import hashlib
>> has digest
>> hashlib.sha256("Classified
Information (007)")
hexdigest()
e224b15d45f4f22cc0c9d395a1eb9993
1ba8b0d2e
# sha224 Digest
>> hashlib.sha224("Classified
Information (007)")
hexdigest()
```

# Seeding random numbers

44 You can use the module
to generate a variety
of random numbers. The *
most used is random.seed([]).
If generator is zero or None,
t current time is used:
current system is also used to
initialise the generator is first.

# "Programming in
Python lets you work more quickly
and integrate your
systems much more effectively"

# Accessing FTP server

41 'ftplib' is a fullyfledged
FTP module for Python. To
establish an FTP connection,nuse the following:

```
smtplib(SMTP, [port])
Example send an email using
Google SMTP server:
```

```
import ftplib(host, [user,
passwd, [act, timeout]])
Example:
```

```
host = "redhat.com"
username = 'anonymous'
password = 'kunaldo@gmail.com'
com
```

+   import ftplib
import urllib2
ftp_serv = ftplib.