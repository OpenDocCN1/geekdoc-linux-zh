Once you select a command, the “Command line” text entry box will get loaded with the command and each of its default arguments separated by exclamation points. In my case I have ARG1 and ARG2. When I look at the command definition, I can see that it passes ARG1 to check_smtp’s –w argument and ARG2 to -c. Most standard Nagios commands use -w and -c to set warning and critical thresholds, respectively, but again you will need to do some research here. In this case they are looking for the number of seconds it takes SMTP to respond to my test. Different SMTP servers have different response times, but I set this to warn me if it takes five seconds to respond, and to send an alert if it takes ten seconds. So in the “Command line” text entry box in place of

```
check_smtp!ARG1!ARG2
```

I put

```
check_smtp!5!10
```

You can see an example of my Service Check tab in Figure 8-7. Now I click Save to save my changes. From this point I can go to the host configuration section and add this check to any hosts I want to monitor. Again, remember to commit your changes to Nagios for them to take effect.

![](bbox=[0.291, 0.596, 0.931, 0.887])

**Figure 8-7** Service Check settings for a new service