
The human senses function only within narrow limits. Sounds can be too soft or too loud to be heard. There are light waves at frequencies lower than the eye can perceive. With our sense of smell we can distinguish among perfume varieties or gag from the stench of a skunk, but we have trouble distinguishing between the scents of two skunks.

As technology causes things to grow smaller, eventually they reach a point where our senses can no longer perceive them. Then a special interface is required for human beings to be able to deal with them. As computers become increasingly sophisticated, the gap between what exists and what the senses perceive widens. The distance between the software carrying out a given task and its user interface becomes an ever-widening void.

The second conclusion we can draw about small things is that, while they do not interface well with people, they tend to interface well with each other. Their small size gives them tremendous flexibility. They are readily suited for integration in many situations.

Consider this example: The next time you see a moving van in your neighborhood, watch how the workers load the customer's belongings. If they're putting an automobile on the van, it goes on first. Then they decide where the next largest pieces go. They follow these with the mid-sized pieces and then the small pieces. The sequence is obvious. But what is really happening is a demonstration that smaller things combine with each other in myriad ways to accomplish a task. While you have some flexibility in the placement of the smaller pieces, the larger ones afford fewer placement choices.

What would happen if you had only small pieces? You would achieve maximum flexibility. This flexibility comes with a price, though. The more small pieces you have, the harder it is for people to deal with them. Managing them becomes a serious problem.

Similarly, in the world of computer software, having many small programs and modules gives you the greatest ability to adapt to the environment. Unfortunately, as the modules get smaller, the issue arises of interacting with the user. The more modules there are, the greater the complexity in dealing with them.

This presents a dilemma for the software designer. He wants maximum flexibility for his application, so he constructs it from a collection of small modules. Yet he is also bound by the requirement that his software be easy to use. People have difficulty dealing with too many small modules.

Unix takes a different approach to resolving this issue. Most other systems try to bridge the ever-widening gap between the user and the module performing the task with a piece of software known as a captive user interface (CUI). Unix developers, on the other hand, recognize that this gap is ever widening. Instead of linking the user and the underlying modules via a mass of "spaghetti" code, they work away at the gap with small chunks or layers.

Since we've just said that Unix and other operating systems diverge on this point, you may suspect that there is an underlying rationale for this. The answer comes from the next tenet of the Unix philosophy.

## 6.1 Tenet 8: Avoid captive user interfaces

Before we begin a discussion of the reasons for avoiding CUIs, we first need to define them. A CUI is a style of interaction with an application that exists outside the scope of the highest-level command interpreter present on the system. Once you invoke an application from the command interpreter, it is not possible to communicate with the command interpreter until the application exits. You are, in effect, held captive within the user interface of the application until you take actions that cause it to release you.

Let’s clarify this with an example. Suppose you have two programs, one that lists the contents of your electronic mailbox and another that searches for a text string in files. If the mail and search programs use CUIs, your interaction might look something like this:

| Command | Description |
| :--- | :--- |
| $ mail | Invoke the *mail* program from the command line. |
| MAIL>dir | Show the contents of the mailbox. |
| MAIL>exit | Exit the *mail* program. Return to command interpreter level. |
| $ search | Invoke the *search* program. |
| SEARCH>find jack *.txt | Perform the search. |
| SEARCH>exit | Exit the *search* program. |
| $ | We’re back at the command interpreter level. |

Notice the flow between the levels here. First, invoking the *mail* command places you inside its own input interpreter. It forces you to interact with its command parser. The parser has a command set different from that of the command interpreter that called it. Second, to execute the *search* command, you must first leave the *mail* command by entering an *exit* command. You then called the *search* command from the main command interpreter. Once you’re inside the *search* application, you must then interact with another command interpreter. This interpreter behaves differently from both the main command interpreter and the *mail* command’s interpreter. The only similarity is that it requires you to enter an *exit* command to end it.

You can see that there are obvious disadvantages with this approach. You must become familiar with three different command interpreters, each with its own interaction language. This may not sound too difficult on a small scale, but it can become prohibitive very quickly on a system that has hundreds of applications. Also, while executing a command, you cannot do anything else until you exit from it. Suppose, for instance, that in responding to a letter in your mailbox, you needed to include some text from another file but you forget which one. You would have to exit from the *mail* command, do the search, and then return to the *mail* application.

So much for the obvious drawbacks. The reasons Unix devotees eschew captive user interfaces are not so obvious. Before we explore these, however, let's contrast this CUI with a Unix-style "noncaptive" interface:

| Command | Description |
| :--- | :--- |
| sh>scan | The `scan` command lists the contents of a mail folder. |
| sh>grep jack *.txt | The `grep` command searches for the string "jack" in all files having names ending in ".txt". |

Notice that the Unix user invokes all commands at the shell prompt or main command interpreter level. Each command completes its task, and control returns to the shell prompt. It is not necessary to exit from each command individually by typing "exit." The user needs to learn only one language—that of the shell, the Unix command interpreter.

The cynic might point out that the user still must learn the order or parameters to be supplied for each command invocation. This is true. But with the CUI, the user must first recall which command to run, then which subcommand to invoke from its CUI. Therefore, there is nearly twice as much to remember. This is not surprising, then, that systems that employ CUIs often must provide highly developed help systems to guide users through the choices. On the other hand, most Unix users get by quite well without complex help systems. Unix commands often return simple messages listing the required parameters and their usage if the user enters an incorrect one.

Thus far, we've defined CUIs and touched upon some of their glaring deficiencies. The real reasons that Unix users avoid them, though, run much deeper. They have to do with the way commands interact with each other. In the Unix environment, no command exists in isolation. Commands interact with each other at various times. CUIs interfere with the ability of multiple commands to make this happen. Multiple command interaction is a key Unix concept.

### 6.1.1 CUIs assume that the user is human

Producers of CUIs base their designs on the premise that a person is sitting at the keyboard. They expect the person to enter responses to the prompts provided by the application. The application then performs calculations or carries out various tasks.

The problem, however, is that even the fastest human being is slower than the average computer. The computer can conduct operations at lightning speed, and it doesn't get tired or take breaks. As stated earlier, people function only within a narrow range. For example, even the speediest typists do not type much more than 80 words per minute. Most CUIs eventually reach a point where the user must respond to a prompt. Then even the fastest supercomputer is little more effective than the lowest PC. Virtually all PCs capture text typed by users without the least bit of strain. As long as a system is constrained to operate within the limits imposed by human beings, it cannot function at its maximum potential.
