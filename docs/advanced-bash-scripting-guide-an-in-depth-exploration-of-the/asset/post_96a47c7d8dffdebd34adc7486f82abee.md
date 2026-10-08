
## Advanced Bash-Scripting Guide

```bash
elif [ "$cur_date" -gt "$pre_date" ]; then
    # If same pkg, but newer,
    pre_date=$cur_date
    pre_file=$cur_file
    #+ update latest pointer.
fi
echo echo \$pre_file >> \$TMP
    # TMP contains ALL
    #+ of refined list now.

    echo "$subshell=\$BASH_SUBSHELL"
    # Bracket required here to let final "echo \$pre_file >> \$TMP"
    # Remained in the same subshell ( 1 ) with the entire loop.

RET=$ # Get return code of the pipe command.

[ "\$RET" -ne 0 ] && {
    echo "List retrieving failed with code \$RET"
    exit \$RET_RETURN
}

echo "done"; echo

# Real rsync download part.
get_file() {
echo "Downloading..."
/bin/nice /usr/bin/rsync \
    \$OPTS \
    --filter merge,+/ \$TMP" \
    --exclude '*' \
    URL \$SRST \
    /usr/bin/tee \$LOG
}

RET=$?

# filter merge,+/ is crucial for the intention.
#+ modifier includes and means absolute path.
# Then sorted in \$TMP will contain ascending dir name and
#+ prevent the following --exclude '*' from "shortcutting the circuit."

echo "Done"
    rm -f \$PID_FILE 2>/dev/null
    return \$RET
}

#
# Main
init
check_pid
set_range
get_list
get_file
RET=$?

if [ "\$RET" -eq 0 ]; then
    /usr/bin/logger -t \$(date) "Fedora update mirrored successfully."
else
    /usr/bin/logger -t \$(date) "*"
fi
```

## 16. External Filters, Programs and Commands

"Fedora update mirrored with failure code: $RET"
fi
nexit $RET

See also [Example A-32].

Using rsync, and similar utilities with security implications in a shell script may not be advisable. Consider, instead, use ssh, scp, or an expect script.

ssh

Secure shell, logs onto a remote host and executes commands there. This secure replacement for telnet, rlogin, rcp, and r uses identity authentication and encryption. See its manpage for details.

### Example 16-4. Using ssh

```bash
#!/bin/bash
# remote.bash: Using ssh.

# This example by Michael Zick.
# Used with permission.
#
# Presumptions:
#n fd-2 isn't being captured ('2>/dev/null').
# ssh/sshd preserves stderr ('2') will display to user.
#n sshd is running on your machine.
# For any 'standard' distribution, it probably is,
+# and without any funky ssh-keygen having been done.
#n Try to ssh your machine from the command-line:
# $ ssh $HOSTNAME
# Without extra set-up you'll be asked for your password.
# enter password
# when done, $ exit

# Did that work? If so, you're ready for more fun.
# Try to ssh your machine as 'root':
# $ ssh -l root $HOSTNAME
# When asked for password, enter root's, not yours.
## Last login: Tue Aug 10 20:25:49 from localhost.localdomain
# Enter 'exit' when done.
#n The above gives you an interactive shell.
# It is possible for sshd to be set up in a 'single command' mode,
+# that is beyond the scope of this example.
# The only thing to note is that the following will work in
+# 'single command' mode.

# A basic, write stdout (local) command.
ls -l

# Now the same basic command on a remote machine.
```

Chapter 16. External Filters, Programs and Commands

```bash
## Pass a different 'USERNAME' 'HOSTNAME' if desired:
USER=$(USERNAME)-$(whoami)
HOST=$(HOSTNAME)-$(hostname)

# Execute the above command-line on the remote host,
## with all transmissions encrypted.

ssh -l ${USER} ${HOST} "ls -l"

# The expected result is a listing of your username's home
## directory on the remote machine.
# To see any difference, run this script from somewhere
## other than your home directory.

# In other words, the Bash command is passed as a quoted line
# to the remote shell, which executes it on the remote machine.
# In this case, ssh does `bash -c "ls -l*"` on your behalf.

# For information on topics such as not having to enter a
## password/passphrase for every command-line, see
## man ssh
## man ssh-keygen
## man sshd_config.
```

Within a loop, ssh may cause unexpected behavior. According to a Usenet post in the complex/unix shell ssh inherits the loop's stdin. To remedy this, pass ssh either by the -n or -f option.

Thanks, Jason Bechtel, for pointing this out.

scp Secure copy, similar in function to rcp, copies files between two different networked machines, but does so using authentication, and with a security level similar to ssh.

### Local Network

### write

This utility allows sending lines to the terminal. It is not applicable to de-activated.

### clear

The clear command simply clears the text at the console or in an xterm. The prompt and cursor reappear at the upper left corner of the screen. This command may be used either at command line or in a script. See Example 11-26.

### reset

Reset terminal parameters and clear text screen. As clear, the prompt and cursor reappear in the upper left corner of the terminal.

### resize

Chapter 16. External Filters, Programs and Commands
