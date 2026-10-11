# ## DESCRIPTION

This tool is part of the *samba*(7) suite.

**nmblookup** is used to query NetBIOS *names* and map them to IP *addresses* in a network using NetBIOS over TCP/IP *port*. The *options* allow the *name* queries to be directed at a particular IP *broadcast* *area* or to a particular *machine*. All *queries* are done over **UDP**.

# ## OPTIONS

+   - **\-M**  Search *for* *a* *master* *browser* *by* *looking* *up* *the* NetBIOS *name* *name* *with* *a* *type* of **0x1d**. If *name* *is* **"\-"** then it does a lookup on the special name **\_MSBROWSE\_.** Please *note* *that* *in* *order* *to* *use* *the* *name* **"\-"**, you need to make sure **"\-"** isn't parsed as an *argument*, *e.g.* *use* : **nmblookup \-M \-\- \-**.

+   - **\-R**  Set *the* *recursion* *desired* *bit* *in* *the* *packet* *to* *do* *a* *recursive* *lookup*. This is used when *sending* *a* *name* *query* *to* *a* *machine* *running* *a* WINS *server* and the user wishes to query the *names* *in* *the* WINS *server*. If *this* *bit* *is* *unset* *the* *normal* (*broadcast* *responding*) NetBIOS *processing* *code* *on* *a* *machine* *is* *used* *instead*. See **RFC1001**, **RFC1002** for *details*.

+   - **\-S**  Once *the* *name* *query* *has* *returned* *an* IP *address* then do a *node* *status* *query* *as* *well*. A *node* *status* *query* *returns* *the* NetBIOS *names* *registered* *by* *a* *host*.

+   - **\-r**  Try *and* *bind* *to* UDP *port* **137** to *send* *and* *receive* UDP *datagrams*. The *reason* *for* *this* *option* *is* *a* *bug* *in* Windows 95 where *it* *ignores* *the* *source* *port* of the requesting *packet* and only *replies* *to* UDP *port* **137**. *Unfortunately*, *on* *most* UNIX *systems* *root* *privilege* *is* *needed* *to* *bind* *to* *this* *port*, *and* *in* *addition*, *if* *the* **nmbd**(8) *daemon* *is* *running* *on* *this* *machine* *it* *also* *binds* *to* *this* *port*.

+   - **\-A**  Interp *ret* *name* *as* *an* IP *Address* *and* *do* *a* *node* *status* *query* *on* *this* *address*.

+   - **\-n**  **<primary NetBIOS name>** This *option* *allows* *you* *to* *override* *the* NetBIOS *name* that Samba *uses* *for* *itself*. This is identical to setting the *parameter* in the **smb.conf** *file*. However, a command line setting will take precedence over settings in **smb.conf**.

+   - **\-i**  **<scope>** This *specifies* *a* NetBIOS *scope* that **nmblookup** *will* *use* *to* *communicate* with when *generating* NetBIOS *names*. For *details* *on* *the* *use* of NetBIOS *scopes*, see **rfc1001.txt** and **rfc1002.txt**. NetBIOS *scopes* *are* *very* *rarely* *used*, *only* *set* *this* *parameter* *if* *you* *are* *the* *system* *administrator* *in* *charge* *of* *all* *the* NetBIOS *systems* *you* *communicate* *with*.