# msghdr

```
struct msghdr {
void	*msg_name;
socklen_t	msg_namelen;
struct iovec	*msg_iov;
size_t	msg_iovlen;
void	*msg_control;
size_t	msg_controllen;
int	msg_flags;
};
```

# cmsghdr

```
struct cmsghdr {
socklen_t	cmsg_len;
int	cmsg_level;
int	cmsg_type;
/*	u_char	cmsg_data[]; */
};
```