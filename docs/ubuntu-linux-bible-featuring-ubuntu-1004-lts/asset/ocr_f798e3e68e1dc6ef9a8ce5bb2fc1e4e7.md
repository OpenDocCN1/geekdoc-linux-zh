# # Backing Up and Restoring Files

Backups are spare copies of the files and directories that are found on a computer system, written to and stored on removable media that is preferably stored other than on your computer. Doing backups are time-consuming, but absolutely mandatory, task if you place any value at all on the files, e-mail, and other data that you have stored on your computer.

Backups are exactly like auto insurance policies—well, almost exactly, because they're not a legal requirement to own a computer system (in most states). You need them, and you hope that you never do. They are usually all just time-consuming and expensive (your time has some value, right?). However, one rainy night when you discover that you've accidentally deleted your home directory or when a user comes to you and says that they've accidentally deleted your company's personnel records, or the source code for your company's products, you'd better have a good answer. The right answer, of course, is "I'll restore that from backups immediately."

It's hard to think of anything that so thoroughly combines the mundane and mandatory as backing up your data. It's boring. And, of course, it's critical. This chapter is oriented toward you as a systems administrator, regardless of how many systems you're responsible for. As system administrators, our responsibility is to provide secure, well-maintained, and rigorously backed-up systems for the benefit of the users of the computer systems we're responsible for. You should feel even more responsible if you're only supporting a user community of one (yourself), because you won't even have anyone to blame if a catastrophe occurs. Even if you're a community of one, I'm sure that you feel that whatever you do on your computer system is important. Backups keep it safe.

# IN THIS CHAPTER

+   * Backups 101

+   * Doing local backups to removable media

+   * Using rsync for remote backups

+   * Using backupcc for site-wide backups

+   * Linux time machines

+   * Backing up and Mirroring to the Cloud