# STEP BY STEP

# 5.5 Verifying and Changing a User's Environment

The following example illustrates how to verify a user's environment settings and how to change them:

1. Log in as the user. This step lets you see the user's environment as the user will see it.

2. Edit the user's initialization files. The following steps suggest some changes and show the shell-specific syntax to use.

3. Set the user's default path to include the home directory and directories or mount points for the user's windowing environment and applications. To change the path setting, add or modify the line for PATH as follows:

For the Bourne or Korn shell, the syntax is as follows:

```
PATH=/dirname1:/dirname2:/dirname3:.; export PATH
```

For example, enter the following line in the user's $HOME/.profile file:

```
PATH=$PATH:/usr/bin:$HOME/bin:/net/glrr/files1/bin:.;export PATH
```

For the C shell, the syntax is as follows:

```
set path =(/dirname1 /dirname2 /dirname3 .)
```

For example, enter the following line in the user's $HOME/.cshrc file:

```
set path=($path /usr/bin $HOME/bin /net/glrr/files1/bin .)
```

4. Check that the environment variables are set to the correct directories for the user's windowing environments and third-party applications. Type env and press Enter:

```
$ env
```

```
HOME=/home/ncalkins
HZ=100
LOGNAME=ncalkins
MAIL=/var/mail/ncalkins
PATH=/usr/bin
```