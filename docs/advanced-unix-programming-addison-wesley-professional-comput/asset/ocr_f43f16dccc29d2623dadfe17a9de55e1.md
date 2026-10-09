```
if (nread == 0) {
    errno = ENETDOWN;
    EC_FAIL
}
if (nread < offsetof(struct smi_msg, smi_data)) {
    errno = EBIG;
    EC_FAIL
}
if ((nclient = clients_find(p,
    (pid_t)p->sq_msg->smi_client.c_idl)) == -1) {
    continue; /* client not notified */
}
if (p->sq_clients[nclient].cl_fd == -1) {
    make_fifo_name_client((pid_t)p->sq_msg->smi_client.c_idl,
    fifo_name, sizeof(fifo_name));
    ec_negl(p->sq_clients[nclient].cl_fd =
    open(fifo_name, O_WRONLY))
    }
    break;
}
else
    ec_negl( nread = read(p->sq_clients[0].cl_fd, p->sq_msg,
    p->sq_msgsizes) )
*addr = p->sq_msg;
return true;

EC_CLEANUP_BGN
return false;
EC_CLEANUP_END
}
```

The one sticky part here is:

```
if ((nclient = clients_find(p, (pid_t)mp->smi_client)) == -1) (
continue; /* client not notified */
)
```

If `clients_find` returns −1, it means that the server got a message from a client but can’t get a slot in the `sq_clients` array so it can’t open the response FIFO. Since it can’t respond, it can’t even send an error message. The example code just ignores the error, leaving the client blocked. Some alternatives would be:

+   - Send a signal to the client, and modify `smi_open_fifo` to arrange to catch it.
+   - Use an integer variable to hold an emergency file descriptor to open the FIFO so an error message can be sent.
+   - At least change the client so it times out rather than staying blocked forever.