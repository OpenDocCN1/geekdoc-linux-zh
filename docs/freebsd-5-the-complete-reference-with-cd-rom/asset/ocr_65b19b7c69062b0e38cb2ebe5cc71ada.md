+   ■ **disconnect script** This option works much like the connect option, but it specifies a command or script to be run upon termination of the link. You might use this option to terminate programs you start in a connection script that's more elaborate than the one shown in Listing 15-1.

+   ■ **connect-max-attempts n** You can tell pppd to attempt to make a connection some specified number of times (n). This option can be useful if your ISP's dial-in lines are frequently busy.

+   ■ **debug** This option is useful if you're having problems; it causes more verbose logging of pppd activities to /var/log/messages.

+   ■ **demand** This option creates a dial-on-demand link, in which pppd initiates a connection when it detects outgoing network traffic.

+   ■ **idle n** This option tells pppd to disconnect a link if it's idle for n seconds or more. This feature can be a useful precaution against accidentally leaving a link active for too long, and it's a practical necessity for use with the demand option.

The pppd program accepts many additional options; consult the pppd man page for more details. In most cases, a configuration file similar to that shown in Listing 15-1 will work well.

# ### Creating a Chat Script

The chat script, referred to as /etc/ppp/chat-script in Listing 15-1, controls the initial connection attempt. In most cases, this script resets the modem, dials it, and waits for a modem connection (which is distinct from the PPP connection that relies upon the underlying modem connection). Listing 15-2 shows a typical chat script. This script is parsed by the /usr/bin/chat program referenced in Listing 15-1. It consists of both option settings specific to chat and a series of expect-send strings—strings that chat is to look for in its input from the modem and strings that it's to send in response. Nominally, chat takes all its options as a single line of input. To make it easier for humans to parse the input, though, it's common to use the backslash (\) line continuation character to break the input into columns. In Listing 15-2, for instance, the first column consists of the expected input and the second column contains the text to send in reply.

> **Listing 15-2**  
> Sample /etc/ppp/chat-script File

```
```
TIMEOUT       30    \ 
ABORT         BUSY  \ 
ABORT         'NO CARRIER' \ 
''            ATZ   \ 
OK            ATDT555-1475 \ 
CONNECT       ''
```
```

![](bbox=[0.88, 0.47, 0.99, 0.62])