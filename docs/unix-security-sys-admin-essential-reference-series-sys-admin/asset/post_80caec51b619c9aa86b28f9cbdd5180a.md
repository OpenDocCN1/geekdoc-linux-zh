
Under certain circumstances, however, it’s useful to be able to delegate some privileges. It may be that a networking staff, rather than the system administrator, is responsible for the networking. Operators may need to back up files. Perhaps a manager has a team of support personnel, but does not want the root password to be that widely known.

This last was the case for a recent customer of mine. The organization had about 500 workstations that were supported by a staff of 20. All these systems had the same root password, which was changed weekly. The major concern was keeping track of what had been done on each of the systems by any of the support personnel. To this end, the root logon was only used when mandatory and was restricted to the system consoles. In place of the root logon, they used a program called sudo (super-user do), which allows them to execute commands with super-user privileges and logs this activity.

## History

sudo (Listing 5.1) is a set-user-id program that runs as root and allows authorized users to execute commands for which they are approved. sudo originally written by Cliff Spencer of SUNY-Buffalo and was published in Evi Nemeth’s UNIX System Administration Handbook. sudo was originally written to run under BSD UNIX.

The original sudo left a number of things undone. These included being able to shell out of programs like vi, using root’s path, having to fully qualify the commands to be executed, having to specify all the commands that can be executed and not being able to specify commands that cannot be executed, and being able to specify "all" commands, thereby allowing a user free range. A user could also sudo a shell and thereby circumvent the logging mechanism.

The original sudo used root’s complete environment, including root’s shell and path. I added the putenv commands to set the shell to /bin/false and assigned a path for commands that can be run by sudo. Reassigning the shell variable keeps programs like vi from being able to spawn a subshell. Assigning a path limits the scope of the commands that can be executed with sudo. It also eliminates the need to fully qualify path names for commands. I added a not option to the configuration file to allow you to configure someone to run all commands except those listed.

### Listing 5.1  The revised sudo.c

```
/*
** sudo.c
*/

/*
** Configurable constants
*/

#define SECURE_PATH "/bin:/usr/bin:/etc"
#define USERFILE "/usr/local/adm/sudoers"
#define LOGFILE "/usr/local/adm/sudolog"
#define TIMEDIR "/usr/local/adm/sudocheck/"
#define TIME 5 /* minutes */
#define SUDO_COP "root@localhost"

/*
** To install create the directories in the SECURE_PATH
** and TIMEDIR and the files USERFILE and LOGFILE.
** Set the owner of these files to root and the permissions
** to og-rw. Change the owner to root for the sudo program
** and set the permissions to 4111 (-s--x--x).
*/

#define BUFSIZE 256
#define SUCCESS 1
#define FAILED -1

#define CONFIG_ERR "Configuration error. Contact your security manager."
#define CONFIG_SUB "Invalid sudo configuration!"
#define SUID_ERR "Set UID bit not set."
#define STAT_ERR "Couldn't stat user file"
#define OWNER_ERR "User file not owned by root"
#define PERM_ERR "Invalid permissions on user file"
#define OPEN_ERR "Couldn't open user file"

#define USER_ERR "You are not set up to execute sudo on this machine."
#define USER_SUB "SECURITY** Invalid sudo user!"

#include <ctype.h>
#include <fcntl.h>
#include <pwd.h>
#include <signal.h>
#include <stdio.h>
#include <string.h>
#include <sys/file.h>
#include <sys/param.h>
#include <sys/stat.h>
#include <sys/time.h>
#include <sys/types.h>
```

### Listing 5.1 (continued)

```
char *getpass();
char *crypt();

FILE *check_config(user)
char *user;
{
    struct stat statb;
    FILE *fp;

    if ((setuid(0)) < 0)                        /* no setuid */
        mail(CONFIG_SUB,user,SUID_ERR,CONFIG_ERR);
    if (stat(USERFILE, &statb))                 /* couldn't stat */
        mail(CONFIG_SUB,user,STAT_ERR,CONFIG_ERR);
    if (statb.st_uid != 0)                      /* must be owned by root */
        mail(CONFIG_SUB,user,OWNER_ERR,CONFIG_ERR);
    if ((statb.st_mode & 044)                   /* should be og-rw */
        mail(CONFIG_SUB,user,PERM_ERR,CONFIG_ERR);
    if ((fp = fopen(USERFILE, "r")) == 0)      /* open err */
        mail(CONFIG_SUB,user,OPEN_ERR,CONFIG_ERR);

    return(fp);
}

char *get_command_list(fp, name, password)
FILE *fp;
char *name;
char *password;
{
    char buffer[BUFSIZ];

    while ((fgets(buffer,BUFSIZ,fp)) != NULL)
    {
        if(buffer[0] == '#') continue;          /* skip remarks */
        if((strncmp(buffer,name,strlen(name))) == 0)
        {
            if (get_password(name,password))   /* valid user */
                return(buffer);
            else
                return(NULL);                   /* invalid password */
        }
    }

    return(NULL);                               /* invalid user */
}
```
