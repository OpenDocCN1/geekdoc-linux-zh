```
return(rendezvous((struct channel *)chan, addr, size, 2));
}

static int rendezvous(struct channel *chan, char *addr,
int size, int sr_flag)
{
    struct message *ptr;
    int nbytes;

    /* 3 */
    if (sr_flag==3-chan->sr_flag)
    {
        /* 4 */
        ptr = chan->message_list;
        chan->message_list = ptr->link;
        ptr->thread->next = current->next;
        ptr->thread->prev = current;
        current->next->prev = ptr->thread;
        current->next = ptr->thread;
        ++thread_count;
        /* 5 */
        nbytes = (size<ptr->size)?size:ptr->size;
        ptr->size = nbytes;

        /* 6 */
        if (sr_flag==1)
            memcpy(ptr->addr, addr, nbytes);
        else
            memcpy(addr, ptr->addr, nbytes);

        /* 7 */
        if (!chan->message_list)
            chan->sr_flag = 0;

        return(nbytes);
    }
    else
    {
        /* 8 */
        ptr = (struct message *)malloc(sizeof(struct message));

        if (!chan->message_list)
            chan->message_list = ptr;
        else
            chan->message_tail->link = ptr;
```