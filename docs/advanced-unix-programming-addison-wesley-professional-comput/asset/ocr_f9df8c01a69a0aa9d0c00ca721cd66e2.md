```
if (p->sq_entity == SMI_SERVER)
ec_negl( mqd_receiver = get_client_mqd(p, p->sq_client.c_idl) )
else {
    mqd_receiver = p->sq_mqd_server;
    p->sq_msg->smi_client.c_id = my_pid;
}
ec_negl( mq_send(mqd_receiver, (const char *)p->sq_msg,
    p->sq_msgsize, 0) )
return true;

EC_CLEANUP_BGN
    return false;
EC_CLEANUP_END
}
```

As before with FIFOs and System V message queues, smi_send_getaddr_mq just saves the client ID (if it’s called from the server) and returns the buffer address. The real work is in smi_send_release_mq. The server calls the lookup function get_client_mqd to get the message-queue descriptor. Its argument was saved in the SMIQ_MQ structure by smi_send_getaddr_mq.

The client already has the server’s descriptor, and it puts its process ID into the message. (The message-queue descriptor can’t be passed between processes, like a System V message-queue identifier can.)

The receive pair are simpler since a receiver already has the descriptor to its message queue:

```
bool smi_receive_getaddr_mq(SMIQ *sqp, void **addr)
{
    SMIQ_MQ *p = (SMIQ_MQ *)sqp;
    mqd_t mqd_receiver;
    ssize_t nrcv;

    if (p->sq_entity == SMI_SERVER)
        mqd_receiver = p->sq_mqd_server;
    else
        mqd_receiver = p->sq_clients[0].c1_mqd;

    ec_negl( nrcv = mq_receive(mqd_receiver, (char *)p->sq_msg,
        p->sq_msgsize, NULL) )
    *addr = p->sq_msg;
    return true;

    EC_CLEANUP_BGN
        return false;
    EC_CLEANUP_END
}
```