```
*
* we really have more the TCP philosophy of urgent data
* rather than the UNIX philosophy of OOB data).
*/
if (n > 1) {
    n = send(net, nbackp, n-1, 0); /* send URGENT all by itself */
} else {
    n = send(net, nbackp, n, MSG_OOB); /* URGENT data */
}

}

if (n < 0) {
if (errno == EWOULDBLOCK)
    return;
/* should blow this guy away... */
return;
}
    nbackp += n;
    if (nbackp >= neturg) {
        neturg = 0;
    }
    if (nbackp == nfrontp) {
        nbackp = nfrontp = netobuf;
    }
}
}

cleanup()
{
    vhangup();  /* XXX */
    shutdown(net, 2);
    exit(1);
}

```

# Macintosh

The Apple Macintosh, the Mac (www.apple.com), with X\_Server is a compelling Internet and/or workgroup server. The core operating system was built using open standards; therefore, the open source software community contributed to its development. Called Darwin, the O/S provides the performance and greater reliability necessary for Internet, publishing, and mission-critical server applications. With new 3D technology, OpenGL, Mac takes the industry’s most widely supported 2D and 3D graphics API to a whole new level.

# Liabilities

Denial-of-Service Attack

**Synopsis:** Remote attack that toggles the Mac Web-sharing functions.

**Hack State:** Configuration control.

**Vulnerabilities:** MacOS 8x.

**Breach:** Sending