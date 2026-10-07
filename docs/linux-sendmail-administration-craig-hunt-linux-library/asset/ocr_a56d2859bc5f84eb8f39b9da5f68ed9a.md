domain. by itself, LOCAL would match wren but not wren. foobirds.org. Combining these two tests in a single rule allows every system in our local domain to use all of the network services.

Use hosts.deny to block login access from all remote systems and use hosts.allow to permit only those computers that you truly want to give login access through the blockade.

# Controlling Network Access with xinetd

An alternative to inetd is xinetd. xinetd is configured in the /etc/xinetd.conf file, which provides the same information as xinetd as inetd.conf provides to inetd. Instead of using positional parameters with meanings determined by location on a configuration line, xinetd.conf uses attribute names that identify the purpose of each parameter. Listing 12.4 shows a sample xinetd conf entry.

# 12.4 An xinetd.conf entry from Red Hat 7

```
# default: on
# description: logind is the server for the login(1) program. \
# The server provides a remote login facility with \
# authentication based on privileged port numbers from \
# trusted hosts.
service login {
  socket_type = stream
  wait = no
  user = root
  log_on_success += USERID
  log_on_failure += USERID
  server = /usr/sbin/in.logind
}
```

The service, socket_type, wait, user, and server values are all parallel values shown in the inetd.conf file, except that the path provided for the server does not invoke the tcp wrapper program. The wrapper is not used because xinetd provides capabilities similar to those of wrapper on its own. xinetd provides its own logging and its access controls.

NOTE The xinetd daemon on Red Hat 7 Linux systems consult the /etc/hosts.allow and /etc/hosts.deny files in addition to the access controls defined in the xinetd.conf file.