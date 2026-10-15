# Looking at Your zsh Configuration Files

Your first step in modifying or adding zsh environment variables in your configuration files, which show you the variables that are explicitly defined. As Code Listing 8.5 shows, you do this using more or the editor of your choice.

Remember that zsh configuration files exist in two places:

+   - Systemwide configuration files (such as /etc/zprofile or /etc/zshenv)
+   - Configuration files specific to your Unix account (such as ~/.zprofile or ~/.zshrc)

```
```
jdoe@usley ~ $ more /etc/z* /etc/z*/zprofile /etc/z*/zshenv


/home/jdoe/.zprofile


# /etc/zprofile and ~/.zprofile are run for login shells


/home/jdoe/.zshenv

export X11HOME=/usr/X11R6


if (( EUID == 0 )); then
  path+=(/sbin /usr/sbin)
fi

typeset -U path
path+=(/path /X11HOME/bin /usr/bin /usr/bin /usr/local/bin)

PATH=$PATH:/home/jdoe/scripts

/home/jdoe/.zshrc

```
```

Code Listing 8.5 Your zsh configuration files set up your environment variables and other features of your Unix experience.

continued on next page