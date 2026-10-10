```
sprintf(string, "Found address for %s\n", hp->h_name);
write(source, string, strlen(string));
} else {
    if (inet_addr(gethost) == -1) {
        found = 0;
        sprintf(string, "Didnt find address for %s\n", gethost);
        write(source, string, strlen(string));
    } else {
        found++;
        sa.sin_addr.s_addr = inet_addr(gethost);
    }
}
} while (!found);
sa.sin_family = AF_INET;
sprintf(string, "Port: ");
write(source, string, strlen(string));
read(source, getport, 100);
gethost[strlen(getport)-2] = '\0';
sa.sin_port = htons(unsigned) atoi(getport));
if (sa.sin_port == 0) {
    sp = getservbyname(getport, "tcp");
    if (sp)
        sa.sin_port = sp->s_port;
    else {
        sprintf(string, "%s: bad port number\n", getport);
        write(source, string, strlen(string));
        return;
    }
}
sprintf(string, "Trying %s...\n", (char *) inet_ntoa(sa.sin_addr));
write(source, string, strlen(string));
if ((dest = socket(AF_INET, SOCK_STREAM, 0)) < 0) {
    perror("telcli: socket");
    exit(1);
}
connect(dest, (struct sockaddr *) &sa, sizeof(sa));
sprintf(string, "Connected to %s port %d... \n",
        inet_ntoa(sa.sin_addr),
        ntohS(sa.sin_port));
write(source, string, strlen(string));
#ifdef FNDELAY
    fcntl(source,F_SETFL,fcntl(source,F_GETFL,0) | FNDELAY);
    fcntl(dest,F_SETFL,fcntl(dest,F_GETFL,0) | FNDELAY);
#else
    fcntl(source,F_SETFL,O_NDELAY);
    fcntl(dest,F_SETFL,O_NDELAY);
#endif
communicate(dest,source);
close(dest);
exit(0);
}
```

347