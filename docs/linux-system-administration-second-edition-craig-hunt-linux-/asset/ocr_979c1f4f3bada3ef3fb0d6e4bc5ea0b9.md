Now that we know how to prevent access to the services available on your system, let's look at how to handle them efficiently with xinetd.

# ## xinetd

You will remember from Chapter 12 that the Internet Services Daemon (inetd) watches all ports assigned to it and starts up the service associated with any port that has activity. This relieves each process of the need to have a daemon running to check these ports. As of Red Hat 7.0, inetd is no longer installed by default. Instead, the more secure extended Internet Service Daemon (xinetd) is used. Most distributions are switching to xinetd as well. Both xinetd and inetd can be run concurrently on a system. In fact, the author of the xinetd code suggests that an admin running an RPC service do so from inetd. You can use your inetd.conf file to create a xinetd.conf file for the non-RPC services.

The biggest reason that xinetd is more secure than inetd is due to its incorporation of something similar to TCP Wrappers. In the xinetd.conf file as well as in the individual /etc/xinetd.d/ files, a number of flags may be set that allow the administrator to determine who may run the service and when they may do so. Listing 12.3 in Chapter 12 showed a sample xinetd service entry. You'll remember that it included a user field to specify what username would be used to start the service. Some services require that the root user control them, but others allow for a different user to control them. If given a choice, always start the program with a non-root user so that any weaknesses in the program behind the service do not render the entire system insecure. Although few services do this by default, it is always good to use the interface flag to specify which interface to listen on for that specific service. If attempts to exploit this service are made on interfaces that aren't explicitly listed, xinetd ignores them instead of being exploited by them. You may use the log-specific flags to alter what information is logged when xinetd runs the specified service. Two more flags important to security are the no_access flag, which lists client machines not to be given access and the only_from flag, which lists all clients authorized to access the service. The use of these flags can help you establish a more secure system.

On a Red Hat 7.3 system, /usr/sbin/inetdconvert is a Python script that converts your inetd.conf file to several files in a new /etc/xinetd.d directory. The command to use this tool to convert all services that haven't already been converted is:

```
`# inetdconvert --convertremaining`
```

A Perl script to convert the inetd.conf script into an xinetd.conf file is included with some other versions of the xinetd package, located in the same directory as the binary. This script will be in /usr/sbin if it exists on your system and may be run using the following command, assuming that the executable is in /usr/sbin:

```
`# /usr/sbin/xconv.pl < /etc/inetd.conf > /tmp/xinetd.conf`
```

The transition creates several files within the /etc/xinetd.d directory. These files contain the configuration options for each service managed by xinetd, so you'll need to edit these files to configure xinetd to handle these services in the way you'd like.

# ## Detecting Intrusion

Intruders usually, if not always, leave signs of intrusion. For some, being noticed is the game. Those who don't want to be noticed need to stay on the system just long enough to adequately mask the intrusion but still get out of the system before someone notices that they are on. Crackers can alter the