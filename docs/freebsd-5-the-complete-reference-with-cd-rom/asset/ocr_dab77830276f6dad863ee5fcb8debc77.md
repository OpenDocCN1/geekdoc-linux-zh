+   - **Look and feel** The modules in this section enable you to set options relating to the user interface of GNOME programs. These options don't apply to most non-GNOME programs, though, so you should not be surprised if they don't affect all your programs.

+   - **Multimedia** You can configure some sound card settings and associate sounds with particular events, such as logging in, logging out, and receiving e-mail.

+   - **Peripherals** You can adjust the keyboard repeat rate, mouse tracking speed, mouse handedness, and similar options with these modules.

+   - **Session** You can set assorted login and logout defaults using the items under the Session option, such as programs you want to launch when you log in and whether GNOME should ask you for confirmation when you log out.

One thing that's important to keep in mind about these configuration options is that they're *user* configuration options. They can vary from one user to another, so several people can use the same computer without having to compromise on options. If Sam really likes a bright pink background, and Sally prefers dark blue, they need not compromise on gray or purple.

Because the GNOME Control Center sets only user options, you can't set some options that affect the entire system. For instance, you can't load drivers, install programs, or format disks from the GNOME Control Center. These actions are administrative tasks that affect the entire system, and they're covered in other chapters of this book.

# Logging Off and Shutting Down

When you're done using FreeBSD, you should do one or both of two things: log off and/or shut down. Logging off leaves the computer running, including any servers you may be running, but it closes access to your account; to use your account, you'll have to log in again. Shutting down the computer is more drastic; it terminates all programs and sends the system into a state in which it's safe for you to turn the computer off.

> **Caution** You should never turn the computer off without first shutting down FreeBSD. Like most modern OSs, FreeBSD performs many operations in the background, and caches disk accesses—that is, it holds onto data before writing it, in the hope of being able to combine the write into one operation, thus improving performance. These characteristics mean that if you simply shut the computer off, you may lose data, and your filesystems may become corrupted. This can slow the boot process and lose even more data.

# Text-Mode and GUI Methods of Logging Off

Logging off prevents people who might wander by from sitting down at the computer and using your account to do things you might not like, such as send offensive e-mail.