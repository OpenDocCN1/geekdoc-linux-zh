```
void add_node(unsigned long sa, unsigned long da, unsigned short sp, unsigned short dp)
{
clistptr newnode;

newnode=(clistptr)malloc(sizeof(struct connection));
newnode->saddr=sa;
newnode->daddr=da;
newnode->sport=sp;
newnode->dport=dp;
newnode->bytes=0;
newnode->next=NULL;
time(& (newnode->start));
time(& (newnode->lasthit));
if (!head)
{
head=newnode;
tail=newnode;
}
else
{
tail->next=newnode;
tail=newnode;
}
}
```

```
char *hostlookup(unsigned long int in)
{
static char blah[1024];
struct in_addr i;
struct hostent *he;

i.s_addr=in;
he=gethostbyaddr ((char *) &i, sizeof(struct in_addr),AF_INET);
if (he == NULL) strcpy(blah, inet_ntoa(i));
else strcpy(blah, he->h_name);
return blah;
}
```

```
char *pretty(time_t *t)
{
char *time;
time=ctime(t);
time[strlen(time)-6]=0;
return time;
}
```

```
int remove_node(unsigned long sa, unsigned long da, unsigned short sp, unsigned short dp)
{
clistptr walker, prev;
int i=0;
```

392