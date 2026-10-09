telnet versus ssh When you connect to a remote UNIX or Linux system using telnet, you are pre- sented with a regular, textual login: prompt. Unless you specify differently, the ssh utility assumes that your username on the remote system matches that on the local system. Because telnet is designed to work with non-UNIX and non-Linux systems, it makes no such assumptions.

# telnet is not secure

> Whenever you enter sensitive information, such as your password, while you are using telnet, it is transmitted in cleartext and can be read by someone who is listening in on the session.

Another difference between these two utilities is that telnet allows you to configure many special parameters, such as how RETURNs or interrupts are processed. When using telnet between UNIX and/or Linux systems, you rarely need to change any parameters.

When you do not specify the name of a remote host on the command line, telnet runs in an interactive mode. The following example is equivalent to the previous telnet example:

```
```
[bravo]$ telnet
 telnet> open kudos
  Trying 172.19.52.2..
  Connected to kudos.example.com
  Escape character is '^]' 
  ..
```
```

Before connecting you to a remote system, telnet tells you what the *escape character* is; in most cases, it is `^]` (where `^` represents the CONTROL key). When you press CONTROL-], you escape to telnet's interactive mode. Continuing the preceding example:

```
```
[kudos]$ CONTROL-]
 telnet> ?

 (displays help information)

 telnet> close
  Connection closed.
 [bravo]$
```
```

When you enter a question mark in response to the telnet> prompt, telnet lists its commands. The close command ends the current telnet session, returning you to the local system. To get out of telnet's interactive mode and resume communication with the remote system, press RETURN in response to a prompt.

You can use telnet to access special remote services at sites that have chosen to make such services available. However, many of these services, such as the U.S. Library of Congress Information System (LOCIS), have moved to the Web. As a consequence, you can now obtain the same information using a Web browser.

# Using telnet to connect to Other Ports

By default telnet connects to port 23, which is used for remote logins. However, you can use telnet to connect to other services by specifying a port number. In addition to standard services, many of the special remote services available on the Internet use unallocated port numbers. For example, you can access some multiplayer text games,