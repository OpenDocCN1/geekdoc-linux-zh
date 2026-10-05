# Infrastructure Protocols 273

Figure 6.87 IP socket glue-router alert handler for user level: linux:/net/ipv4/ip.sockglue.c.

```
// Special input handler for packets caught by router alert option.
They are selected only by protocol field, and processed likely
local ones; but only if someone wants them! Otherwise, router
running ravpd will keep RSVP.

It is user level problem, what it will make with them.
I have no idea how it will masquerade or NAT them (it is joke, joke :->));
but receiver should be enough cfe. to forward trace requests,
sent to multicast group to reach destination designated router.
/
struct ip_ra_chain *ip_ra;
rwlock_t ip_ra_lock = RW_LOCK_UNLOCKED;

ip_ra_control(struct sock *sk, unsigned char ra, void (*destructor)) (struct sock *))
{
	struct ip_ra_chain *new_ra, *rap;

	if (sk->type == SOCK_RAW || sk->num == IPPROTO_RAW)
	eturn -EINVAL;
	}
	new_ra = kmalloc(sizeof(new_ra), GFP_KERNEL) : NULL;
```

Figure 6.88 IP socket glue-router alert handler for user level: linux:/net/ipv4/ip.sockglue.c.

```
write_lock_bh(&ip_ra_lock);
for (rap = &ip_ra_chain->ra, ra=**rap; rap != NULL; ra = &ra->next) {
	if (ra->sk == sk) {
		if (con) {
			write_unlock_bh(&ip_ra_lock);
			if (new_ra)
				kfree(new_ra);
				returnreturn -EADDRINUSE;
		}
		rap = ra->next;
		write_unlock_bh(&ip_ra_lock);

	if (ra->destructor) {
			ra->destructor(sk);
			sock_put(sk);
			kfree(sk);
			return 0;
		}
	}	if (new_ra == NULL) {
		write_unlock_bh(&ip_ra_lock);
		return -ENOBUFS;
}

new_ra->sk = sk;
new_ra->destructor = destructor;
```