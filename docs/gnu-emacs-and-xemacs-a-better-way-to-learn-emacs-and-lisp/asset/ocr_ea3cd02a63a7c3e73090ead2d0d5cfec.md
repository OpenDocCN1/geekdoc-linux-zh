![](bbox=[0.19, 0.08, 0.79, 0.36])

# figure 22.1 GNU Emacs Messages Buffer

Another source of information that can be useful at times is the *lssage*. This is another of those peculiar Emacs terms that doubtless has its origin in the "dark backward and abysm of time" from which Emacs arose. It simply means the last hundred characters you have typed, rendered in a literal way, including M-x commands, spaces, and keystroke commands. The top window in Figure 22.1 shows a Lssage buffer.

Why would you want to see this? If you type a command and Emacs behaves strangely, you can take a look at this buffer and see what you actually typed, rather than what you think you typed. The buffer can be summarized by pressing M-x and typing

```
view-lssage
```

or by pressing Ctrl-1.

This isn't a command you will use daily, but every now and then it can clear up a murky situation.

# **XEmacs and Recent Messages**

On the XEmacs Help menu, you will find an item called **Recent Messages**. When you select this, you see a buffer resembling Figure 22.2.

The XEmacs version has the lssage characters at the top of the buffer with the message log just below, combining the two GNU Emacs buffers just described.