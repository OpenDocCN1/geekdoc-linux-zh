You can also change this variable in the nnmail-expire Customize group.

You can manually expire a message at any time by pressing E in the Summary buffer. If it’s a big file and you want to dispose of it at once rather than wait until the expiration happens, just press B Delete.

The following Lisp statement can be used as a template to fine-tune expiration periods for several mail folders. Check your parentheses well!

```
(setq nnmail-expiry-wait-function

(lambda (group)

(cond ((string= group "family") 60)

((string= group "junk") 1)

((string= group "main") 'never)

(t 9))

))
```

This chunk of Lisp creates a lambda (nameless) function, the main body of which is a conditional statement that says if the string “family” matches a mail folder’s name, wait 60 days before expiring the messages. The expiry action to take with the main folder is never, which disables expiry completely for that folder. Don’t forget the single quote before never, because it prevents the Lisp interpreter from trying to make sense of the word. It needs to be passed unaltered to Gnus. Another valid entry rather than an integer or the word never is immediate, which signals Gnus that you want all messages in a folder expired right now.

# Attachments and MIME

All you need to do to attach a file to an outgoing message is press Ctrl-c Ctrl-a (or use the menu). You are asked for a file name (Tab completion comes in handy) and a MIME type. A default type is suggested.

When you receive a message with a MIME attachment, Gnus should know what to do with it. If you’d rather use external viewers for images, or if you need to have a certain type of MIME type passed to another application, you can use keyboard commands.

The MIME-related commands are numerous, but these few will handle most of your needs: