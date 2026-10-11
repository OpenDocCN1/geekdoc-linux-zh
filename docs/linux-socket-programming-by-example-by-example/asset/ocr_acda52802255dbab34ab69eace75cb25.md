Datagram servers obtain the client's address from the recvfrom(2) function. The following is a code excerpt from Listing 6.1:

```
int z;
struct sockaddr_in adr_clnt;/* AF_INET */
int len_inet;
/* Length */
int s;
/* Socket */
char dgram[512];
/* Recv buffer */
```

```
len_inet = sizeof adr_clnt;
z = recvfrom(s,
/* Socket */
dgram,
/* Receiving buffer */
sizeof dgram,
/* Max recv buf size */
0,
/* Flags: no options */
(struct sockaddr *)&adr_clnt,
/* Addr */
&len_inet);
```

After the client's address has been obtained in either type of server, you then apply the techniques from Chapter 9, “Hostname and Network Name Lookups,” using the gethostbyaddr(3) function. Here is another code excerpt from Listing 9.8 to review how a client's IP number is resolved to a hostname:

```
struct sockaddr_in adr_clnt;/* AF_INET */
struct hostent *hp;
/* Host entry ptr */
```

```
hp = gethostbyaddr(
(char *)&adr_clnt.sin_addr,
sizeof adr_clnt.sin_addr,
adr_clnt.sin_family);
```

```
if (!hp)
fprintf(logf, " Error: %s\n",
hstrerror(h_errno));
else
fprintf(logf, " %s\n",
hp->h_name);
```

After the server has the fully qualified hostname in hp->h_name, it is able to apply any grant or deny policy that the program designer wants.

# ### Identifying by IP Number

Although it is convenient for humans to work with system hostnames and domain names, there are security problems associated with this method of identification. When the IP number is received by the server, it must then use another network process (initiated by gethostbyaddr(3) ) to resolve that number into a hostname. It is quite conceivabe that the attacker has set