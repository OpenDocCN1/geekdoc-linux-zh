A user or group ID is just some number. If you want a name, you have to call `getpwuid` or `getgrgid`, which were described in Section 3.5.2. Here's an example program that displays the real and effective user and group IDs:

```
```
int main(void)
{
	uid_t uid;
	gid_t gid;
	struct passwd *pwd;
	struct group *grp;

	uid = getuid();
	if ( (pwd = getpwuid(uid)) != NULL )
		printf("Real user = %ld (%s)\n", (long)uid, pwd->pw_name);

	uid = geteuid();
	if ( (pwd = getpwuid(uid)) != NULL )
		printf("Effective user = %ld (%s)\n", (long)uid, pwd->pw_name);

	gid = getgid();
	if ( (grp = getgrgid(gid)) != NULL )
		printf("Real group = %ld (%s)\n", (long)gid, grp->gr_name);

	gid = getegid();
	if ( (grp = getgrgid(gid)) != NULL )
		printf("Effective group = %ld (%s)\n", (long)gid, grp->gr_name);

	exit(EXIT_SUCCESS);

CLEANUP_BEG
	exit(EXIT_FAILURE);
CLEANUP_END
}
```
```

To make the output interesting, I changed the user and group owners of the program file (`uidgrp`) and then turned on the set-ID-on-execution bits for the user and group:

```
```
$ su
Password:
# chown adm:sys uidgrp
# chmod +s uidgrp
$ uidgrp
Real user = 100 (marc)
Effective user = 4 (adm)
Real group = 14 (sysadmin)
Effective group = 3 (sys)
$ 
```
```