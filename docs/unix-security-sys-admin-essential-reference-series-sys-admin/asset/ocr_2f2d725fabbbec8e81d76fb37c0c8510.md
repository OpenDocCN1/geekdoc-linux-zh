# How sudo Works

sudo first validates its configuration. It checks that it is owned by root and has the set-UID bit set. It checks the configuration file to validate that it is not writeable or readable by anyone other than root (the configuration file contains the list of authorized users and the commands that they can execute). sudo next validates the user, by scanning through the configuration file to find the user's logon name, and the command that was entered, by scanning the list of commands that are valid for that user.

# Listing 5.1 (continued)

```
int get_password(name, password)
char *name;
char *password;
{
    char fname[200];
    char *pswd;
    char *encrypted;
    struct stat stab;

    sprintf(fname, "%s/%s", TIMEDIR, name);

    if (stat(fname, &stab) == 0)
    {
        if ((time(NULL) - stab.st_mtime) < (TIME * 60))
        {
            create_file(fname);
            return (SUCCESS);
        }
    }

    pswd = getpass("Password:");
    encrypted = crypt(pswd, password);

    if (strcmp(password, encrypted))
    {
        fprintf(stderr, "Password incorrect\n");
        return (FAILED);
    }
    fflush (stderr);
    fflush (stdout);

    create_file(fname);
    return (SUCCESS);
}
```