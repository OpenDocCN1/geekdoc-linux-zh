keyboard. Therefore, you want to sit at `apolllo` and run programs that are located on `zeus`. Both systems run Linux. To accomplish this task, follow these steps:

+   1. Log into `apolllo` and, if it’s not already running X, start it.
+   2. Open a terminal (such as an `xterm`) on `apolllo`.
+   3. Type `xhost +zeus` in `apolllo`’s terminal. This command tells `apolllo` to accept for display in its X server data that originates on `zeus`.
+   4. Log into `zeus` from `apolllo`. You might use Telnet or Secure Shell (SSH), for instance. The result should be the ability to type commands in a shell on `zeus`.
+   5. On `zeus`, type `export DISPLAY=apolllo:0.0`. (This assumes you’re using bash; if you’re using `tcsh`, the command is `setenv DISPLAY apolllo:0.0`) This command tells `zeus` to use `apolllo` for the display of X programs. (Chapter 9, “Writing Scripts, Configuring E-Mail, and Using Databases,” describes environment variables, such as `DISPLAY`, in greater detail.)
+   6. Type whatever you need to type to run programs at the `zeus` command prompt. For instance, you could type `office` to launch OpenOffice.org. You should see the programs open on `apolllo`’s display, but they’re running on `zeus`—their computations use `zeus`’s CPU, they can read files accessible on `zeus`, and so on.
+   7. After you’re done, close the programs you’ve launched, log off `zeus`, and type `xhost -zeus` on `apolllo`. This tightens security so that a miscreant on `zeus` won’t be able to modify your display on `apolllo`.

# Real World Scenario

Encrypting X Connections with SSH

The SSH protocol is a useful remote-access tool. Although it’s often considered a text-mode protocol, SSH also has the ability to tunnel network connections—that is, to carry another protocol through its own encrypted connection. This feature is most useful for handling remote X access. You can perform the steps described in “Using Remote X Clients” but omit steps 3 and 5 and the xhost command in step 7. This greatly simplifies the login process and adds the benefits of SSH’s encryption, which X doesn’t provide. On the other hand, SSH’s encryption is likely to slow down X access, although if you enable SSH’s compression features, this problem may be reduced in severity. Overall, tunneling X through SSH is the preferred method of remote X access, particularly when any network in the process isn’t totally secure.

SSH tunneling does require that certain options be set. In particular, you must either use the -X option to the ssh client program or set the ForwardX11 option to yes in /etc/ssh_config on the client system. You must also set the X11Forwarding option to yes in the /etc/sshd_config file on the SSH server system. These options enable SSH’s X forwarding feature; without these options, SSH’s X forwarding won’t work.