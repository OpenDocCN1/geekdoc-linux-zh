![](bbox=[0.38, 0.038, 0.9, 0.571])

Figure 17.3  Rmail-Filtered Summary

When you click the middle mouse button on a message in a Summary buffer, the message appears in another window. When you read a message, the spacebar pages down and the Delete key pages up. (The Page Up and Page Down keys also work.)

One advantage Rmail has over VM is that it has an extensive Customize interface. Press M-x and type

```
customize-group
```

Respond to the prompt with

```
rmail:
```

You will find in these nested menus many Rmail variables to examine or change.

# Rmail Output and Labels

Rmail offers a nice variety of commands for dealing with messages. You can save messages to files in either standard UNIX mailbox format or in Rmail's Babyl format: