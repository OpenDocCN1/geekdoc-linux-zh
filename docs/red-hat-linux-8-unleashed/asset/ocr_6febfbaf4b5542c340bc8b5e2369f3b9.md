# Using Smart Hosts

If you don't have a full-time connection to the Internet, you will probably want to have Sendmail send your messages to your ISP's mail server and let it handle delivery for you. Without a full-time Internet connection, you could find it difficult to deliver messages to some locations (such as some underdeveloped areas of the world where email services are unreliable and sporadic). In those situations, you can configure Sendmail to function as a smart host by passing email to another sender rather than attempting to deliver it directly. You can use a line such as the following in the sendmail.mc file to enable a smart host:

```
define('SMART_HOST', 'smtp.samlenenet.org')
```

This causes Sendmail to pass any mail it receives to the server smtp.samlenenet.org rather than attempt to deliver it directly. Smart hosting won't work for you if your ISP, like many others, blocks any relaying. Some ISPs block relaying because it's frequently used to dispatch spam.

# Setting Message Delivery Intervals

As mentioned earlier, Sendmail typically attempts to deliver messages as soon as it receives them, and at regular intervals after that. If you have only periodic connections to the Internet, as with a dial-up connection, you would likely prefer that Sendmail hold all messages in the queue and attempt to deliver them at specific time intervals or at your prompt. You can configure Sendmail to do so by adding the following line to sendmail.mc:

```
define('DELIVERY_MODE', 'd')1
```

This will cause Sendmail to only attempt delivery at regularly scheduled queue processing intervals (by default, somewhere between 20 and 30 minutes).

However, this delay time might not be sufficient if you're offline for longer periods of time. In those situations, you can invoke Sendmail with no queue processing time. For example, by default, Sendmail might start with the following command:

```
# sendmail -bd -q30m
```

This tells Sendmail that it should process the mail queue (and attempt message delivery) every 30 minutes. You can change 30 to any number to change the delivery interval. If you want Sendmail to wait for a specific prompt before processing the queue, you can invoke Sendmail with no queue time, like this:

```
# sendmail -bd -q
```