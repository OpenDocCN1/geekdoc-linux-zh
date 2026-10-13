Now use the `faxstat` command to check the status of the daemons as follows:

```
```text
# faxstat
HylaFAX scheduler on orion.bwc.org: Running
Modem ttyS1 (+972.4.8331039): Running and idle
```
```

You should see output similar to the above.

# SENDING A TEST FAX MESSAGE

On the fax server host create a quick test message as follows:

```
```text
# cat > /tmp/testfax
This is a fax message to test the newly installed HylaFAX server.
FaxMaster
^D
```
```

Now use the sendfax command to send this test message to a remote fax machine or server as follows:

```
```text
# sendfax -n -D -d 8358525 /tmp/testfax
```
```

It is not necessary to prepare a fax file ahead of time; sendfax can input from the standard input also. To use standard input to deliver a message to sendfax use the following command:

```
```text
# sendfax -n -D -d 8358525 <
This is a fax message to test the newly installed HylaFAX server.
FaxMaster
^D
```
```

Remember to use a different destination fax number instead of the one shown in the example.

Here’s what the various flags used in the example mean:

+   - `-n`: This tells sendfax to not send a cover page.
+   - `-D`: This tells sendfax to email the status after the job is done.
+   - `-d`: This flag is followed by the destination fax number.

Once you have sent the message, check the status of the fax server with the faxstat command as follows:

```
```text
# faxstat
HylaFAX scheduler on orion.bwc.org: Running
Modem ttyS1 (+972.4.8331039): Sending job 1
```
```

A status report similar to the above should be printed. Run faxstat again after a minute or so and you should see something like the following:

```
```text
# faxstat
HylaFAX scheduler on orion.bwc.org: Running
Modem ttyS1 (+972.4.8331039): Running and idle
```
```

In addition to the status you just checked using faxstat to verify the message was sent successfully, you should receive a status report emailed to you by the fax server. Check the root user’s mailbox and there should be a message similar to the following: