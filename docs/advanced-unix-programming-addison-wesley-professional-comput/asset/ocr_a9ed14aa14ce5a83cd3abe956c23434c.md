```
```c
bool smi_send_release_shm(SMIQ *sqp)
{
    SMIQ_SHM *p = (SMIQ_SHM *)sqp;
    int semid_receiver;

    if (p->sq_entity == SMI_SERVER)
        semid_receiver = p->sq_client.c_id2;
    else
        semid_receiver = p->sq_sem_id_server;
    ec_neg( op_semi(semid_receiver, SEMI_READ, SEMI_POST) )
    return true;

EC_CLEANUP_BGN
    return false;
EC_CLEANUP_END
}
```
```

All this function needs to do is post the `SEMI_READ` semaphore, but to do that it needs the semaphore-set identifier. For the server, it’s in the `client_id` that smi_send_getaddr_shm stored in the SMIQ_SHM structure; for the client we had it in that structure from the start.

At this point you should be able to follow smi_receive_getaddr_shm pretty easily:

```
```c
bool smi_receive_getaddr_shm(SMIQ *sqp, void **addr)
{
    SMIQ_SHM *p = (SMIQ_SHM *)sqp;
    int semid_receiver;

    if (p->sq_entity == SMI_SERVER)
        semid_receiver = p->sq_sem_id_server;
    else
        semid_receiver = p->sq_sem_id_client;
    ec_neg( op_semi(semid_receiver, SEMI_READ, SEMI_WAIT) )
    if (p->sq_entity == SMI_SERVER)
        *addr = p->msg_server;
    else
        *addr = p->msg_client;
    return true;

EC_CLEANUP_BGN
    return false;
EC_CLEANUP_END
}
```
```

The corresponding function smi_receive_release_shm has to post the