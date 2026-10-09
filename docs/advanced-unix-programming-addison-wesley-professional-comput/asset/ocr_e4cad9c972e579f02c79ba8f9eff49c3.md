want to keep track of its clients anyway. The client will only use the first element of the array to store its own message-queue descriptor, but we don’t care about wasted space in this example.

There are two functions to translate SMI server names and client process IDs to POSIX IPC names:

```
static void make_mq_name_server(const SMIO_MQ *p, char *mqname,
           size_t mqname_max)
{
    snprintf(mqname, mqname_max, "/smmq-%s&", p->sq_name);
}

static void make_mq_name_client(pid_t pid, char *mqname,
           size_t mqname_max)
{
    snprintf(mqname, mqname_max, "/smimq-c%d", pid);
}
```

These names look like they’re in the root directory, but on Solaris they’re not, as explained in Section 7.6.2.

Next comes a function used by the server to get a client’s message-queue descriptor from its process ID, which is what a client sends in a message to the server:

```
static mqd_t get_client_mqd(SMIQ_MQ *p, pid_t pid)
{
    int i, avail = -1;
    char mqname[SERVER_NAME_MAX + 100];

    for (i = 0; i < MAX_CLIENTS; i++) {
        if (p->sq_clients[i].cl_pid == pid)
            return p->sq_clients[i].cl_mqd;
        if (avail == -1 && p->sq_clients[i].cl_pid == 0)
            avail = i;
    }

    errno = ECONNREFUSED;
    ec_negl_t avail )
    p->sq_clients[avail].cl_pid = pid;
    make_mq_name_client(pid, mqname, sizeof(mqname));
    ec_negl( p->sq_clients[avail].cl_mqd = mq_open(mqname, O_WRONLY) )
    return p->sq_clients[avail].cl_mqd;

EC_CLEANUP_BGN
    return (mqd_t) -1;
EC_CLEANUP_END
}
```