
facilities reserved for graduate students and faculty. rma is also used to prevent users who are not members of systems staff from logging into the department’s servers. Listing 6.1 is the current version of the rma code.

The rma code restricts access by moving the shells (typically found in /bin and /usr/bin) to a new location — the directory specified by the SHELL_DIR define in the program. /usr/bin/shells is usually a good choice. For security reasons, the statically linked copy of the Bourne shell (usually found in /sbin) should remain untouched, because it is customarily root’s login shell. Then, the original shell names are linked to the rma binary, which should be copied to /usr/bin. This same procedure is used to install most wrapper programs.

## Listing 6.1 (continued)

```
/* Print access violation message and send email with /usr/ucb/Mail */
/* if configured to do so. */
void KickOut(void)
{
    int in;

    printf("Access to this machine RESTRICTED!!\\n");

#ifdef MAIL_TO
    if((in = open("/dev/null", O_RDONLY, 777)) != 0) {
        dup2(in, 0);
        execl("/usr/ucb/Mail", "Mail", "-s", "ACCESS VIOLATION", MAIL_TO, NULL);
        exit(1);
    }
#endif

    /* M A I N   P R O G R A M */
    main (int argc, char ** argv)
    {
        char host[MAXHOSTNAMELEN];
        uid_t gid;

        /* Block some signals */
        signal(SIGINT, SIG_IGN);
        signal(SIGTERM, SIG_IGN);

        /* Determine our hostname */
        if (gethostname(host, MAXHOSTNAMELEN))
            perror("Who am I...get me HELP!");

        /* Get the user's primary gid */
        gid = getgid();

        /* Start the user's shell if */
        /* access is allowed */
        if(CanLogin(gid, host))
            Login(argv);
        else
            KickOut();
    }
```

## Enforcing Access Restrictions

Enforcement of access restrictions is based on the system's hostname and the user's primary group ID. These policies are specified by creating a file containing access lists. The name and location of this file are determined by the definition of ACCESS_LIST. Each machine running rma must have an ACCESS_LIST that is owned by root with file permissions 644. The format of this file closely resembles a standard UNIX group file, which allows rma to use the fgetgrent() function to process the file. This feature greatly reduces the amount of code required for rma. However this similarity with the group file also has a disadvantage: there is no method for adding comments to the ACCESS_LIST.

rma looks in the equivalent of the password field for a + or a - character to determine the type of access list given for a group. A + indicates an allow list (i.e., a list of machines that group members may use), whereas a - denotes a deny list (i.e., a list of machines group members may not access). Figure 6.4 shows an ACCESS_LIST that

- 1. allows wheel and daemon group members to access any machine by denying access to no machines;
- 2. permits the staff group login access only to the machines named isis, bast, and horus;
- 3. restricts the sales group from logging into isis;
- 4. prohibits users with a primary group of guest from logging into any machine by not granting access to any machines.

The wheel and daemon groups, along with any other system-level groups, should be given access to all machines in a domain. Otherwise, root access may possibly be disabled, along with that of other administrative users. Although giving each machine an ACCESS_LIST that describes the entire domain may seem redundant, this method does ease administration. When changes are required, a new access file can be distributed to all machines with a utility like rdist. This method of updating the access list helps to preserve the NIS paradigm of centralized management, which rma does not directly support.

### Figure 6.4 A sample ACCESS_LIST file specifies which users can access which machines.

```
wheel:-:0:
daemon:-:1:
staff:+:300:isis,bast,horus
sales:-:101:isis
guest:+:101:
```
