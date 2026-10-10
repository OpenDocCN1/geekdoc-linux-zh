application.

So much for the obvious drawbacks. The reasons Unix devotees eschew captive user interfaces are not so obvious. Before we explore these, however, let's contrast this CUI with a Unix-style "noncaptive" interface:

| sh>scan | The `scan` command lists the contents of a mail folder. |
|---|---|
| sh>grep jack *.txt | The `grep` command searches for the string "jack" in all files having names ending in ".txt". |
| : | : |
| : | : |

Notice that the Unix user invokes all commands at the shell prompt or main command interpreter level. Each command completes its task, and control returns to the shell prompt. It is not necessary to exit from each command individually by typing "exit." The user needs to learn only one language-that of the shell, the Unix command interpreter.

The cynic might point out that the user still must learn the order or parameters to be supplied for each command invocation. This is true. But with the CUI, the user must first recall which command to run, then which subcommand to invoke from its CUI. Therefore, there is nearly twice as much to remember. This is not surprising, then, that systems that employ CUIs often must provide highly developed help systems to guide users through the choices. On the other hand, most Unix users get by quite well without complex help systems. Unix commands often return simple messages listing the required parameters and their usage if the user enters an incorrect one.

Thus far, we've defined CUIs and touched upon some of their glaring deficiencies. The real reasons that Unix users avoid them, though, run much deeper. They have to do with the way commands interact with each other. In the Unix environment, no command exists in isolation. Commands interact with each other at various times. CUIs interfere with the ability of multiple commands to make this happen. Multiple command interaction is a key Unix concept.

# 6.1.1 CUIs assume that the user is human

Producers of CUIs base their designs on the premise that a person is sitting at the keyboard. They expect the person to enter responses to the prompts provided by the application. The application then performs calculations or carries out various tasks.

The problem, however, is that even the fastest human being is slower than the average computer. The computer can conduct operations at lightning speed, and it doesn't get tired or take breaks. As stated earlier, people function only within a narrow range. For example, even the speediest typists do not type much more than 80 words per minute. Most CUIs eventually reach a point where the user must respond to a prompt. Then even the fastest supercomputer is little more effective than the lowest PC. Virtually all PCs capture text typed by users without the least bit of strain. As long as a system is constrained to operate within the limits imposed by human beings, it cannot function at its maximum potential.