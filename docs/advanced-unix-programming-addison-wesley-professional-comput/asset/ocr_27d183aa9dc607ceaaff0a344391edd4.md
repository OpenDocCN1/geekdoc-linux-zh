We'll see these calls in the smi_open_fifo and smi_close_fifo functions.

When the server gets a message, it uses clients_find to see if it already has a file descriptor open to the FIFO, and to find an available slot if not:

```
static int clients_find(SMIQ_FIFO *p, pid_t pid)
{
    int i, avail = -1;

    for (i = 0; i < MAX_CLIENTS; i++) {
        if (p->sq_clients[i].cl_pid == pid)
            return i;
        if (p->sq_clients[i].cl_fd == -1 && avail == -1)
            avail = i;
    }
    if (avail != -1)
        p->sq_clients[avail].cl_pid = pid;
    return avail;
}
```

This function returns -1 if no more clients can be handled.

The final internal functions are for making the FIFO names. The server's is fixed, while the clients' contain their process IDs, just as in the earlier example in Section 7.2.2.

```
static void make_fifo_name_server(const SMIQ_FIFO *p, char *fifo_name,
                                  size_t fifoname_max)
{
    snprintf(fifo_name, fifoname_max, "/tmp/smiq_fifo-%s", p->sq_name);
}

static void make_fifo_name_client(pid_t pid, char *fifo_name,
                                  size_t fifoname_max)
{
    snprintf(fifo_name, fifoname_max, "/tmp/smiq_fifo%d", (long)pid);
}
```

Now we're ready to look at smi_open_fifo:

```
SMIQ *smi_open_fifo(const char *name, SMIENTITY entity, size_t msgsize)
{
    SMIQ_FIFO *p = NULL;
    char fifoname[SERVER_NAME_MAX + 50];

    ec_null( p = calloc(1, sizeof(SMIQ_FIFO)) )
    p->sq_msgsize = msgsize + offsetof(struct SMI_msg, smi_data);
    ec_null( p->sq_msg = calloc(1, p->sq_msgsize) )
    p->sq_entity = entity;
```