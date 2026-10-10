```
continue;
}
if(FD_ISSET(tapfd, &rfds)) {
    FD_CLR(tapfd, &rfds);
    if((len = read(tapfd, buffer, BUFSIZE)) < 1) {
        if(len == -1)
            perror("read_tapfd");
        printf("tapfd died, quitting\n");
        shutdown(netfd, 2);
        close(netfd);
        exit(0);
    }
    printf("%d bytes from interface\n", len);
    write(netfd, buffer, len);
    continue;
}
}  /* end of looping */
}
void usage(void) {
    printf("Wrong arguments.\n");
    exit(0);
}

```

```
/* fwtunnel uses ethertap to tunnel an address
   fwtunnel <host | -> <port>
   the first argument is either the hostname to connect to, or, if
   you're the host which will be listening, a -. obviously, the
   system inside the firewall gives the hostname, and the free system
   gives the -.
   both sides must specify a port #...   this should, clearly, be the
   same for both ends...
   */
   /* for linux --
   first, you'll need a kernel in the later 2.1 range.
   in the "Networking Options" section, turn on:
   "Kernel/User netlink socket"
   and, just below,
   "Netlink device emulation"

```

353