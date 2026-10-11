The lines starting with **ib**: indicate in-band data that was written. The line beginning with `OOB` indicates that 'rejected' was written as out-of-band data to the socket.

If you were able to watch both sessions at the same time, you will notice that the receiving program reports the data shortly after it is sent by the sending program. Its session output should look like this:

```
$ ./oobrec v
rcv 'In the beginning' (16)
rcv 'Linus begat Linux,' (18)
rcv 'and the Penguins' (16)
URG 'd' (1)
rcv 'rejoice' (7)
rcv 'exceedingly.' (12)
$
```

The output lines shown in this terminal session that begin with `rcv` indicates normal in-band data that was received. The line starting with `URG` indicates that `SIGURG` was raised and the signal handler was called. Within the signal handler, the urgent data is read and reported. You should notice something peculiar—only the *d* byte was received as out-of-band data! What gives? Read on to find out.

# ## Understanding the Urgent Pointer

Early in this chapter, it was stated that the socket interface provides a general network interface. This includes how it deals with out-of-band data. The TCP implementation of urgent data, however, falls somewhat short of what a general concept might include for out-of-band data.

Although the entire string 'rejoiced' was sent as out-of-band data using `send(2)`, the following observations can be made at the receiving end:

+   - Only the *d* character was received as out-of-band data.
+   - The *d* character was received ahead of the remaining characters in 'rejoice'.

The fact that the *d* byte was received ahead of the bytes 'rejoice' does indeed demonstrate that the *d* byte was more urgent. It shows that the byte ordering has been disturbed by an urgency factor.

# ## Understanding TCP Urgent Mode

The fact that only one byte was received as out-of-band data has to do with the mapping of a TCP protocol concept to a socket concept. The TCP *urgent mode* is mapped to the more general socket concept of out-of-band data.