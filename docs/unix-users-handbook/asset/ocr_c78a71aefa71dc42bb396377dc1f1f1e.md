This **mail** session is typical. We first used **mail** to invoke the electronic mail program. We are informed that there is one message from *tomf* with the subject *12:00 Phone Call*. We then use ? to get a list of **mail** commands. I selected this particular system for the **mail** examples because of the clear help messages that are produced with ?. We then use *t* to display the message we received, *R* to reply to *tomf* the sender of the message, *s* to save and delete the message, and finally quit with *q*. A file called **mbox** has been produced that contains all of the saved messages.

You can see from this example how easily you can handle the messages in your mailbox. It may be, however, that you wish to view summary information of the messages you have saved and deleted. The file **mbox** in my home directory was created to store messages that were saved and then deleted. We can view summary information of these messages using the option "-f" and **mbox** as an input file as shown in the following example:

```
```text
martyp $ mail -f mbox
Mail [5.2 UCB] Type ? for help.
"mbox": 4 messages
 1 tomf             Sun Sep 26 18:14   11/343   "Training"
>2 donnak           Mon Sep 27  07:23   12/402   "Performance"
 3 carollync        Mon Sep 27  07:27   12/380   "Software Update"
 4 tomf             Mon Sep 27  07:38   11/357   "12:00 Phone Call"```
```

You can see in this example that there were four messages saved in **mbox** that we can work with simply by specifying the number of the file (1-4). The current message is indicated by the right arrow >. Information is available on the date and time of delivery of the message, the size of the message in lines and characters, and the subject of the message. Saving and deleting files with *s* ensures that a copy of the file is maintained so that you can later access it.

A slightly more advanced electronic mail program is on some systems, called **mailx**. When run, **mailx** produces a list of messages for you rather than displaying them one at a time as **mail** does. The **mailx** list of messages is similar to the list we just saw with deleted