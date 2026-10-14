There are various complications with receiving and processing messages, since every type of communication is different, both in how the text format is used and the way in which messages are picked up the system. In Chapter 5 you saw examples of how e-mail and SMS require significantly different code to process the incoming message.

My approach is to let the software that receives the communication in the very first instance (the web or e-mail server, for example) to authenticate the user. Most of these daemons will be running as a privileged user of some description and therefore less vulnerable to abuse. In addition to deducing the Minerva-oriented user account of the sender, the receiving code will also be in charge of stripping out all message information that is not pertinent (in the form of header, footers, signatures, and so on) before sending a much-reduced command to your msgsrcv script. This pushes the workload to where it belongs and gives your script a unified appearance to all input conduits.

Taking the example of SMS, you already have a web page in place that is invoked whenever someone sends a message to your house. This page might process the input and call the receiver script using the following:

```
```sh
$command = "/usr/local/minerva/bin/msgsrcv sms ";
$command .= $_POST['from'];
$command .= " ";
$command .= $_POST['text'];

system($command);
```
```

which evaluates down to a command such as the following:

```
```text
msgsrcv sms 012345678 bedroom on
```
```

The command code can then look up the phone number in $INBASE/etc/msg/sms/addr/alias and deduce who is issuing the command and whether they’re allowed to use it.

From here you can determine how to process the command and its arguments in a uniform way. However, allowing arbitrary access to the entire Linux command set is very dangerous, particularly given the privileges under which software such as the web server is run. As you’ve just seen, even the seemingly inconspicuous SMS control requires Apache and is therefore vulnerable. Therefore, each user has a list of applications it is allowed to use, as controlled with the minuser command.

Furthermore, you can kill two proverbial birds with one stone by preparing your own set of aliases. Some commands, like kettle, are short and simple and effective for SMS messages. Others such as the following are not:

```
```text
homedevice default on bedroom_light
```
```

Consequently, you will create a directory /usr/local/minerva/etc/msg/sms/cmd that contains a number of command scripts which sort names. bedroom, for example, would perform the full command given earlier. You could also create an aliased command called sleepover, which runs the following:

```
```text
homedevice default off bedroom_light
homedevice default off studio_light
homedevice default off lounge_light
```
```

This would eliminate a lot of typing and limit the scope for command injection attacks. This also allows you to add new SMS-controllable commands without changing the SMS input handler code inside the web directory.

Notice that in this example and all others like it, you always pass the actual command type and address through to the underlying script as you did with msgxmit. You suffer no performance penalty for doing so, and it ensures that error reports are sent back to the correct user, using the same conduit.