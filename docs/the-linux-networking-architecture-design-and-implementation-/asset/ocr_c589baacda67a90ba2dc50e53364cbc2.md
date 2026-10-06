# 596 Appendix G Example for Communication over Sockets

```
* Signal handler to accept the SIGCHLD signal when terminating
* child processes; otherwise, these zombie processes would remain.
/
```

```
void sighandler(int dummy)
{
    wait(NULL);
}
```

```
/* Function to serve a client:
* Read available characters from socket into the buffer.
* Search for end-of-line character; if found, or if buffer full:
* output message, move the rest forward, and repeat.
* Abort, if error, or connection closed.
/
```

```
void serve(int s, struct sockaddr_in *peer)
{
    int space, n;
    char *p, *q;
    q = p = buf; space = BUFSIZE;
    while (1) {
        if ((n = read(s, p, space)) <= 0) break;
        p += n; space -= n;
        while ((q < p) && (*q != '\\n')) q++;
        while ((q < p) || !*q) {
            *q = 0;
            printf("message from %d.%d.%d.%d: %s\n",
                NIPQUAD(peer->sin_addr.s_addr), ntohs(peer->sin_port), buf);
            if (q < p) q++;
            memmove(buf, q, p - q);
            n = q - buf; // Number of characters "done"
            p -= n; space += n;
            q = buf;
            while ((q < p) && (*q != '\\n')) q++;
        }
}
```

```
if (n < 0) perror("read");
else if (p > buf) { // Output rest
    *p = 0;
    printf("message from %d.%d.%d.%d: %s\n",
        NIPQUAD(peer->sin_addr.s_addr), ntohs(peer->sin_port), buf);
}
```

```
/* Main program:
* Process arguments
* Open socket and wait for connections
* Start separate process for each new connection
/
```

```
int main(int argc, char *argv[])
{
```