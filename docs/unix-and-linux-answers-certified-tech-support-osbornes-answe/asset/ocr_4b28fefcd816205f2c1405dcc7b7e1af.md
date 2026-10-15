and you want to be able to send messages back and forth without causing each other problems, designate a specific window for "chatting" with each other. We like to use ttypl as our chat window, and we keep it open but in the background. When a message comes in to that window, we get a beep and we just click on the window to pop it up to the top.

# How can I chat with another user who is on a different machine?

Use the talk command. talk also writes directly to your screen, but it will split the screen into two separate halves, one for what you are writing and one for what is being sent to you by the other user. Even more than with the write command, you need to be sure that the person receiving the request to talk isn't in the middle of something else. However, you can talk to a person on another machine in your workgroup just as easily as if that person were simply on another terminal attached to your machine. To chat with another user, the syntax is

```
talk username@hostname
```

where username is their login name, and hostname is their machine's name as defined in the hosts table.

# Can I send a message to everyone who is logged in to my computer?

Yes, with the wall command. Be aware, however, that it won't cross over to other machines, so you can't really use it to send a message to everyone on the network. In a traditional UNIX environment with a single large server and lots of terminals connected to it, this works perfectly. But in today's more modern distributed workstation environment, you'll have to use one of the mail commands to reach everyone in your workgroup.