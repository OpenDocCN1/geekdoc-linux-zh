unwanted access from outside hosts, such as those sending spam mail. A basic client or server Sendmail configuration involves just a few features in the `/etc/mail/sendmail.mc` file. The default Fedora configuration installed on your system allows use on a single host, managing messages between users on that host. To enable client and server use, you will need to make changes to the `/etc/mail/sendmail.mc` file.

# Configuring Sendmail for a Simple Network Configuration

Fedora initially configures Sendmail to work only on the system it is running on, **localhost**. To use Sendmail to send messages to other hosts on a local network, you need to change and add settings in the `sendmail.mc` and `/etc/mail/access` files. A simple network configuration would have Sendmail running on each host, handling both mail sent between users on that host and mail to and from users on other hosts. For each Sendmail server configuration, you would make the changes described in the following section on simple local network configuration.

For messages sent between hosts on your network, you only need to run the Sendmail server on each, making a few changes to their Sendmail configurations. The Sendmail server on one of your hosts can be configured to handle the task of relaying messages between hosts. Using the network example described earlier, the hosts **turtle**, **rabbit**, and **lizard** will be running their own Sendmail servers. The Sendmail server on the **turtle** host will be configured to relay messages between all the hosts, itself included.

On each host on your network, edit the `/etc/mail/sendmail.mc` file and make the following changes. Comment out the DAEMON_OPTIONS line in the default `sendmail.mc` file by placing a `dn1` word in front of it, as shown here. Removing this feature will allow you to receive messages over your local network. This entry is restricting Sendmail to the **localhost** (127.0.0.1):

```
dn1 DAEMON_OPTIONS(`Port=smtp,Addr=127.0.0.1, Name=M`TA')dn1
```

In the `sendmail.mc` file located on the host that you want to have handle the relaying of messages, you need to also add the following line:

```
FEATURE(relay_entire_domain)dn1
```

Run the `m4` operation to install the changed configuration and then restart the server with the service operation, as described earlier.

You can now e-mail messages from one user to another across your network. For example, **george@turtle.mytrek.com** can now e-mail a message to **larisa@rabbit.mytrek.com**. The local Sendmail servers will take care of sending and delivering mail both to users within their hosts and those located on other network hosts.

# Configuring Sendmail for a Centralized Mail Server

Alternatively, you could set up a central mail server to handle all the mail on your network. Mail clients on various hosts could send their messages to the central mail server, which would then relay them out to the larger network or Internet. Mail could then be received at the central mail server, where clients could later retrieve it. There are several ways to set up a central mail server. One of the simplest is to run a central mail server on your gateway host, and then have null client versions of the Sendmail server running on local hosts.