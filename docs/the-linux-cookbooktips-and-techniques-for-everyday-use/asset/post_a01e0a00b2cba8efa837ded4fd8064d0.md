
## 3.4 Running a Command

| KEYSTROKE | DESCRIPTION |
|---|---|
| ALT-Fn | Switch to virtual console *n*, where *n* is a number from 1 to 7 (the default maximum). |
| CTRL-ALT-Fn | When in X, switch to virtual console *n*, where *n* is a number from 1 to 6. |
| ALT-← | Switch to the next-lowest virtual console. For example, typing this while in virtual console 4 switches to virtual console 3. Pressing this keystroke in the lowest console wraps around to the highest console. [GNU INFO BUG: any <> in the preceding line should be the one of the cursor arrow keys.] |
| ALT-→ | Switch to the next-highest virtual console. For example, typing this while in virtual console 4 switches to virtual console 5. Pressing this keystroke in the highest console wraps around to the lowest console. [GNU INFO BUG: any <> in the preceding line should be the one of the cursor arrow keys.] |
| SHIFT-PgUp | Scroll back one screen to view previously displayed text. |
| SHIFT-PgDn | When viewing previously displayed text, scroll forward one screen. |

A *tool* is a software program that performs a certain function—usually a specialized, simple task. For example, the `hostname` tool outputs the system's hostname, and the `who` tool outputs a listing of the users who are currently logged in. An *application* is the name given to larger, usually interactive, programs for completing broader kinds of tasks—such as programs for image editing or word processing.

A tool or application may take any number of *options* (sometimes called "flags"), which specify a change in its default behavior. It may also take *arguments*, which specify a file or some other text to operate on. Arguments are usually specified after any options.

A *command* is the name of a tool or application along with the options and arguments you want to use, if any. Since typing the name of a tool itself is often sufficient to accomplish a desired task, tools alone are often called commands.

Commands are case sensitive; the names of tools and applications are usually in all lowercase letters.

To run (or "execute") a tool or application without giving any options or arguments, type its name at a shell prompt followed by RET.

- To run the `hostname` tool, type:

```
$ hostname RET
bardo
$
```

The hostname of the system in the example is `bardo`.

## The Linux Cookbook: Tips and Techniques for Everyday Use:

Options always begin with a hyphen character, ` - `, which is usually followed by one alphanumeric character. To include an option in a command, follow the name of the tool or application with the option. Always separate the tool name, each option, and each argument with a space character.

Long-style options (sometimes called "GNU-style" options) begin with two hyphen characters (` -- `) and are usually one English word.

For example, many tools have an option, `--version`, to output the version number of the tool. (Many tools also have a `--help` option, which outputs a list of options the tool takes; see section Listing the Usage of a Tool.)

- To output the version of the hostname tool, type:

```
$ hostname --version RET
hostname 2.10
$
```

This command outputs the text `hostname 2.10`, indicating that this is version 2.10 of the hostname tool.

Sometimes, an option itself may take an argument. For example, hostname has an option for specifying a file name to use to read the hostname from, `-F`; it takes as an argument the name of the file that hostname should read from.

- To run hostname and specify that the file `host.info` is the file to read from, type:

```
$ hostname -F host.info RET
```

## 3.5 Changing Your Password

To change your password, use the passwd tool. It prompts you for your current password and a new password to replace it with. For security purposes, neither the old nor the new password is echoed to the screen as you type it. To make sure that you type the new password correctly, passwd prompts you for your new password twice. You must type it exactly the same way both times, or passwd will not change your password.

- To change your password, type:

```
$ passwd RET
Changing password for kurt
```
