So, if your machine is **fred** and the remote machine is **barney**, your machine would set name **fred** remotename **barney** and the remote machine would set name **barney** remotename **fred** in their respective /etc/ppp/options. ttySx files.

The /etc/chap-secrets file for fred would look like

```
# Secrets for authentication using CHAP
# client    server secret    acceptable local IP addresses
fred        barney flintstone.
barney      fred wilma
```

and for barney

```
# Secrets for authentication using CHAP
# client    server secret    acceptable local IP addresses
barney      fred flintstone
fred        barney wilma
```

Note in particular that both machines must have entries for bi-directional authentication. This allows the local machine to authenticate itself to the remote *and* the remote machine to authenticate itself to the local machine.

# # Handling Multiple PAP-Authenticated Connections

Some users have more than one server to which they connect that use PAP. Provided that your user name is different on each machine to which you want to connect, this is not a problem.

However, many users have the same user name on two (or more—even all) systems to which they connect. This then presents a problem in correctly selecting the appropriate line from /etc/ppp/pap-secrets.

As you might suspect, PPP provides a mechanism for overcoming this. PPP allows you to set an “assumed name” for the remote (server) end of the connection using the **remotename** option to pppd.

Let us suppose that you connect to two PPP servers using the user-name *fred*. You set up your /etc/ppp/pap-secrets something like

```
fred  pppserver1  barney
fred  pppserver2  wilma
```

Now, to set connect to pppserver1 you would use name **fred** remotename **pppserver1** in your ppp-options and for pppserver2 name **fred** remotename **pppserver2**.