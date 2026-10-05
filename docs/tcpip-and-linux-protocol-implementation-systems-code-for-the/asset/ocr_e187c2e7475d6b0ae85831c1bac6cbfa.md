# Protocol Implementation Framework 169

```
918 int fd1, fd2, err;
```

```
919
```

```
920 /
 * Obtain the first socket and check if the underlying protocol
 * supports the socketpair call.
 */
```

```
925 err = sock_create(family, type, protocol, &sock1);
if (err < 0)
 goto out;
```

```
929 err = sock_create(family, type, protocol, &sock2);
if (err < 0)
 goto out_release_1;
```

```
933 err = sock_ops->socketpair(sock1, sock2);
if (err < 0)
 goto out_release_both;
```

```
937 fd1 = fd2 -1;
```

Figure 5.94 Socket glue-create a socket pair: linux/net/socket.c.

```
939 err = sock_map_fd(sock1);
if (err < 0)
 goto out_release_both;
fd1 = err;
```

```
944 err = sock_map_fd(sock2);
if (err < 0)
 goto out_close_1;
fd2 = err;
```

```
949 /* fd1 and fd2 may be already another descriptors.
 * Not kernel problem.
 */
```

```
953 err = put_user(fd1, &sockvec[0]);
if (err)
 err = put_user(fd2, &sockvec[i]);
if (err)
 return 0;
```

```
959 sys_close(fd2);
sys_close(fd1);
return err;
```

```
963 out_close:
sock_release(sock2);
sys_close(fd1);
return err;
```

```
968 out_release_both;
```