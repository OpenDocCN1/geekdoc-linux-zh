# An Introduction to the vi Editor

Now try using the Backspace and Return keys to see how they help you move around.

+   4. Move to the middle of a line:

| total 29 | 512 Nov 21 10:39 Archives/ |
| drwx----- | 2 taylor 512 Dec 3 02:03 Infolorld/ |
| drwx----- | 2 taylor 1024 Dec 3 01:43 Mail/ |

Here, I at the mid digit in the file size of the second file in the listing. Here are a couple of new cursor motion keys: The 0 (zero) key moves the cursor to the beginning of the line, and $ moves it to the end of the line. First, I type:

| total 29 | 512 Nov 21 10:39 Archives/ |
| drwx----- | 3 taylor 512 Dec 3 02:03 Infolorld/ |
| drwx----- | 2 taylor 1024 Dec 3 01:43 Mail/ |

Now I type$ to move to the end of the line:

| total 29 | 512 Nov 21 10:39 Archives/ |
| drwx----- | 3 taylor 512 Dec 3 02:03 Infolorld/ |
| drwx----- | 2 taylor 1024 Dec 3 01:43 Mail/ |

+   5. If you have arrow keys on your keyboard, try to see them if they work the same way that the h, j, k, and l keys work. If the arrow keys don't move you, they might have shifted you into insert mode. If you type characters and they're added to the file, you need to press the Escape key (or Esc, depending on your keyboard) to return to command mode. Let's wrap this up by leaving this session. Because vi now knows that you have modified the file, it will try to ensure that you don't quit without saving the changes:

```
~~
:qnNo write since last change (:quit! overrides)
```

![](bbox=[0.878, 0.453, 0.967, 0.547])