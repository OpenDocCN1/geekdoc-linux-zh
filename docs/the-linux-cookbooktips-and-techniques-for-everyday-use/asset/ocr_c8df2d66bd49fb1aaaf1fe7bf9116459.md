# 3.4 Running a Command

| KEYSTROKE | DESCRIPTION |
|---|---|
| ALT-Fn | Switch to virtual console *n*, where *n* is a number from 1 to 7 (the default maximum). |
| CTRL-ALT-Fn | When in X, switch to virtual console *n*, where *n* is a number from 1 to 6. |
| ALT-@leftarrow | Switch to the next-lowest virtual console. For example, typing this while in virtual console 4 switches to virtual console 3. Pressing this keystroke in the lowest console wraps around to the highest console. [GNU INFO BUG: any <> in the preceding line should be the one of the cursor arrow keys.] |
| ALT-@rightarrow | Switch to the next-highest virtual console. For example, typing this while in virtual console 4 switches to virtual console 5. Pressing this keystroke in the highest console wraps around to the lowest console. [GNU INFO BUG: any <> in the preceding line should be the one of the cursor arrow keys.] |
| SHIFT-PgUp | Scroll back one screen to view previously displayed text. |
| SHIFT-PgDn | When viewing previously displayed text, scroll forward one screen. |

A *tool* is a software program that performs a certain function—usually a specialized, simple task. For example, the `hostname` tool outputs the system's hostname, and the `who` tool outputs a listing of the users who are currently logged in. An *application* is the name given to larger, usually interactive, programs for completing broader kinds of tasks—such as programs for image editing or word processing.

A tool or application may take any number of *options* (sometimes called "flags"), which specify a change in its default behavior. It may also take *arguments*, which specify a file or some other text to operate on. Arguments are usually specified after any options.

A *command* is the name of a tool or application along with the options and arguments you want to use, if any. Since typing the name of a tool itself is often sufficient to accomplish a desired task, tools alone are often called commands.

Commands are case sensitive; the names of tools and applications are usually in all lowercase letters.

To run (or "execute") a tool or application without giving any options or arguments, type its name at a shell prompt followed by RET.

+   - To run the `hostname` tool, type:

```
$ hostname RET
bardo
$
```

The hostname of the system in the example is `bardo`.