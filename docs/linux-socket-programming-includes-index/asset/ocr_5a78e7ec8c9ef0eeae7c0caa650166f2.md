If you want to send an urgent message, you need to use the MSG_OOB option in the send() system call. Additionally, like asynchronous I/O, you need to enable capturing this event with a system call to fctl():

```
/*** Claim ownership of SIGIO and SIGURG signals ***/
/*** Can't claim SIGURG and SIGIO ***/
if ( fcntl(sockfd, F_SETOWN, getpid()) != 0 )
    perror("Can't claim SIGURG and SIGIO");
```

This call tells the kernel that you want to get asynchronous notification of SIGURG and SIGIO. Remember that the call uses only one byte of message as the OOB data.

You can use the urgent (OOB) messages to make sure that the listener is alive, because unlike regular data, flow control does not block them. You might use this for a heartbeat:

```
/****** Heartbeat between programs: Server replying to beats ****/
/*** ('heartbeat-server.c' on Web site) ****/
int clientfd;

void sig_handler(int signum)
{
    char c;
    if ( signum == SIGURG )
    {
        recv(clientfd, &c, sizeof(c));
        if ( c == '?')               /* Are you alive? */
            send(clientfd, "Y", 1, MSG_OOB);  /* YES! */
    }
}

int main()
{
    int sockfd;
    struct sa_action act;
    bzero(&act, sizeof(act));
    act.sa_handler = sig_handler;
    saction(SIGURG, &act, 0);       /* connect SIGURG signal */

    /*** set up server & connection client to clientfd ***/
    /* --claim SIGIO/SIGURG signals--- */
    if ( fcntl(clientfd, F_SETOWN, getpid()) != 0 )
        perror("Can't claim SIGURG and SIGIO");
    /*** do your work ****/
}
```