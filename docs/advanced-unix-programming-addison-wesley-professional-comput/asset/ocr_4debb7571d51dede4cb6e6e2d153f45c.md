```
EC_CLEANUP_BGN
return -1;
EC_CLEANUP_END
}
```

There's also a handy function to initialize a semaphore:

```
static int init_semi(int semid)
{
    union semun arg;
    int r;

    arg.val = 0;
    semctl(semid, SEMI_WRITE, SETVAL, arg);
    semctl(semid, SEMI_READ, SETVAL, arg);
    /* Following call will set o time, allowing clients to proceed. */
    ec_neg!({ r = op_semi(semid, SEMI_WRITE, SEMI_POST) })
    return r;

EC_CLEANUP_BGN
return -1;
EC_CLEANUP_END
}
```

This is the internal data structure behind the SMIQ type that the SMI uses:

```
typedef struct {
    SMIENTITY sq_entity;      /* entity */
    int sq_semID_server;      /* server sem */
    int sq_semID_client;      /* client sem (client only) */
    int sq_shmID_server;      /* server shm ID */
    int sq_shmID_client;      /* client shm ID (client only) */
    struct smi_msg *msg_server; /* ptr to server shm */
    struct smi_msg *msg_client; /* ptr to client shm (client only) */
    char sq_name[SERVER_NAME_MAX]; /* server name */
    struct client_id sq_client; /* client identification (server only) */
} SMIQ_SHM;
```

A client uses almost the whole structure, but the server just uses some of the members. A client stores:

+   * Its entity (SMI_CLIENT) and the server name
+   * The semaphore-set IDs (2 semaphores each) for itself and the server
+   * The shared-memory segment IDs for itself and the server
+   * Pointers (from shmact) to its and the server's segments

The server stores: