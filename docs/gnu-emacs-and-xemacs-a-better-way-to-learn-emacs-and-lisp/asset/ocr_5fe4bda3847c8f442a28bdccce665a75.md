![](bbox=[0.04, 0.09, 0.67, 0.4])

# **Figure 10.8     Gnus Agent Groups**

Using this command, you can be selective about about which group's messages are downloaded.

When your downloads are complete, select Toggle plugged from the Agent menu or type

```
`J J`
```

Now Gnus is in its “unplugged” state and doesn't care whether you are connected to the Internet.

You can read the new messages just as you do in a normal Gnus session but without tying up a phone line. Messages marked as read are subject to the normal expiration process, and you can use any of the usual Gnus commands for saving, making persistent, and so on.

You might have noticed that nearly all Agent key commands begin with a capital J. As an aid to remembering them, the letters that follow the J are often the same as the analogous Gnus commands.

When the Gnus Agent is enabled, you can still use the original startup command M-x *gnus* if you are already connected to the Internet. You will still be able to “unplug” at any time, whether you are connected or not.