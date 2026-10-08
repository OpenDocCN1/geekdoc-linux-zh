
```bash
echo SERVER_PROTOCOL = $SERVER_PROTOCOL
echo SERVER_PORT = $SERVER_PORT
echo REQUEST_METHOD = $REQUEST_METHOD
echo HTTP_ACCEPT = "HTTP_ACCEPT"
echo PATH_INFO = $PATH_INFO
echo PATH_TRANSLATED = $PATH_TRANSLATED
echo SCRIPT_NAME = $SCRIPT_NAME
echo QUERY_STRING = $QUERY_STRING
echo REMOTE_HOST = $REMOTE_HOST
echo REMOTE_ADDR = $REMOTE_ADDR
echo REMOTE_USER = $REMOTE_USER
echo AUTH_TYPE = $AUTH_TYPE
echo CONTENT_TYPE = $CONTENT_TYPE
echo CONTENT_LENGTH = $CONTENT_LENGTH
```

```bash
exit 0
```

# Here document to give instructions.
<='_test_CGI_'

- 1) Drop this in your http://domain.name/cgi-bin directory.
2) Then, open http://domain.name/cgi-bin/test-cgi.sh.

_test_CGI_
For security purposes, it may be helpful to identify the IP addresses a computer is accessing.

# Example 30-2. IP addresses

```bash
#!/bin/bash
# ip-addresses.sh
# list the IP addresses your computer is connected to.

# Inspired by Greg Bledsoe's ddos.sh script,
# Linux Journal, 09 March 2011.
# URL:
# http://www.linuxjournal.com/content/back-dead-simple-bash-complex-ddos
# Greg licensed his script under the GPL
# and as a derivative, this script is likewise GPL2.
```

```bash
connection_type=TCP # Also try UDP.
field=2 # Which field of the output we are interested in.
no_match=LISTEN # Filter out records containing this. Why?
lsof_args=-ni # -i lists Internet-associated files.
# -n preserves numerical IP addresses.
# What sharpens without the -n option? Try it.
router="[0-9] [0-9] [0-9] [0-9]"
# Delete the router info.
```

```bash
lsof "$lssof_args" | grep "$connection_type" | grep -v "$no_match*"
awk '{print $1}' | cut -d ' ' -f $field | sort | uniq
sed 's/$//'
```

```bash
# Bledsoe's script assigns the output of a filtered IP list,
# (similar to lines 19-22), to a variable.
# He checks for multiple connections to a single IP address,
# then uses:
```

```bash
iptables -I INPUT -s $ip -p tcp -j REJECT --reject-with tcp
```

Chapter 30. Network Programming

```bash
# ... within a 60-second delay loop to bounce packets from DDOS attacks.

# Exercise:
# -----
# Use the 'iptables' command to extend this script
#+ to reject connection attempts from well-known spamer IP domains.
```

More examples of network programming:

- 1. Getting the time from nist.gov
- 2. Downloading a URL
- 3. A GRE tunnel
- 4. Checking if an Internet server is up
- 5. Example 16-41
- 6. Example A-28
- 7. Example A-29
- 8. Example 29-1

See also the networking commands in the System and Administrative Commands chapter and the communications commands in the External Filters, Programs and Commands chapter.

# Chapter 31. Of Zeros and Nulls

> Faultily faultless, icily regular, splendidly null

Dead perfection; no more.

--Alfred Lord Tennyson

```bash
/dev/zero ... /dev/null
```

Uses of /dev/null
Think of /dev/null as a black hole. It is essentially the equivalent of a write-only file. Everything written to it disappears. Attempts to read or output from it results in nothing. All the same, /dev/null can be quite useful from both the command-line and in scripts.

Suppressing stdout.

```bash
cat $filename >/dev/null
# Contents of the file will not list to stdout.
```
Suppressing stderr (from Example 16-3).

```bash
rm $badname 2>/dev/null
# So error messages [stderr] disappear.
```
Suppressing out both stdout and stderr.

```bash
cat $filename 2>/dev/null /dev/null
# If "$filename" does not exist, there will be no error message output.
# If "$filename" exists, the contents of the file will not list to stdout.
# Therefore, no output at all will result from the above line of code.

# This can be useful in situations where the return code from a command
# needs to be tested, but no output is desired.

cat $filename &>/dev/null
# also works, as Baris Cisek points out.
```

Deleting contents of a file, but preserving the file itself, with all attendant permissions (from Example 2-1 and Example 2-3).

```bash
cat /dev/null /var/log/messages
# > /var/log/messages has same effect, but does not spawn a new process.
cat /dev/null /var/log/wtmp
```

Automatically emptying the contents of a logfile (especially good for dealing with those nasty "cookies" sent by commercial web sites:

# Example 31-1. Hiding the cookie jar

```bash
# Obsolete
# This script is no longer used.
```

Chapter 31. Of Zeros and Nulls

Advanced Scripting Guide
