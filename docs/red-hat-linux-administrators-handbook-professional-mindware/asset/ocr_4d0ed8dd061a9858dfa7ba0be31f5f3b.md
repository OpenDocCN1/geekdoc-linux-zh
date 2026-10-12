Returning to the first example scenario, where you have two assistants who don't yet need full superuser access, suppose that you (user ID = yourid) want these two users (sysad1, sysad2) to have privileges to run only the shutdown command. In such a case, your `/etc/sudoers` file might look like this:

```
# User alias specification
User_Alias SENIORADMIN=yourid
User_Alias ASSISTANTS=sysad1,sysad2

# User privilege specification
SENIORADMIN ALL=ALL
ASSISTANTS ALL=/sbin/shutdown
```

Suppose that after a while, you become confident that these two users can handle other superuser privileges in a responsible manner, so you want to give them full access except for the privilege to run the su command. The `/etc/sudoers` file now looks as follows:

```
# User alias specification
User_Alias SENIORADMIN=yourid
User_Alias ASSISTANTS=sysad1,sysad2

# User privilege specification
SENIORADMIN ALL=ALL
ASSISTANTS ALL=ALL, !/bin/su
```

As you can see from the user specifications for the `ASSISTANTS`, they are allowed to run ALL commands via sudo except for the `/bin/su` command.

# ## Managing Users with Command-Line Tools

This section shows you the traditional way of doing user administration using various command-line tools.