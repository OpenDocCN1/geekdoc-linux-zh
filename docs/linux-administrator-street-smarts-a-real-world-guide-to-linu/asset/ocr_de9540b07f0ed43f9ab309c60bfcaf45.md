you should know how to set passwords that are hard to break. Just as important, your **users** should know how to set good passwords. Thus, you should share the techniques described in this task with your users to improve your *overall* system security.

![](bbox=[0.15, 0.18, 0.23, 0.27])

> The mainstream media uses the term **hacker** to refer to computer miscreants. This word has an older and more honorable meaning, though: In the Linux world, *hacker* often refers to people who are skilled with computers, and particularly with computer programming, and who use their skills for productive purposes. Many Linux developers consider themselves hackers in this positive sense. Thus, I use another word, *cracker*, to refer to individuals who break into and otherwise disrupt the operation of computers.

The same rules that apply to user passwords apply to the **root** password, but the **root** password is even more critical. Thus, you should be particularly diligent about setting a good **root** password, keeping it secret, and changing it from time to time.

# ## Scenario

As part of routine security maintenance, you want to change both your user password and your **root** password. Phase 1 describes the `passwd` utility, which is used to change your password; but to use this tool most effectively, you need to know how to generate a good password—or *two* good passwords, one for your user account and one for the computer’s **root** account. (Ordinary users without superuser access need only generate one good password for each computer, of course.)

# ## Scope of Task

This task is basically a mental one; it can be done without access to a computer. Of course, in *practice* you’ll ultimately need to use your Linux system and its `passwd` utility to change your password.

# ## Duration

This task should take half an hour or less to complete. Once you’re familiar with the techniques of password generation, you should be able to create a new one in under a minute.

# ## Setup

No special setup is required to complete this task; you can do it using your mind alone (and this book for reference). To actually set your password, of course, you’ll need to log into your Linux system and use the `passwd` utility.

# ## Caveats

As a purely mental activity, password generation poses no particular risks *per se*. The risks really apply to the consequences of doing this task incorrectly. A poor password might be