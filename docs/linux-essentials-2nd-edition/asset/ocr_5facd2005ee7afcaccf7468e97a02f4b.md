# CHAPTER 12

# Understanding Basic
Security

**Linux is a multiuser OS**, meaning that it provides features to help mul-ntiple individuals use the computer. Collectively, these features constitute **accounts**. Previous chapters of this book have referred to accounts in passing but haven't covered them in detail.

This chapter changes that; it describes important account principles and a few commands that you can use to begin investigating accounts. Related to accounts are **groups**, which are collections of accounts that can be given special permissions on the computer, so this chapter also describes groups. One account, known as **root**, has special privileges on the computer. You use this account to perform most system administration tasks, so you should understand this account before you tackle the administrative tasks described in the last few chapters of this book. These important topics are at found-ation of system security.

+   - Understanding accounts
- Using account tools
- Working as root

# Understanding Accounts

Accounts enable multiple users to share a single computer without caus-ing other too much trouble. They also enable system administrators to track who is using system resources and, sometimes, who is doing things they shouldn't be doing. Account features help users use a computer and administrators administer it. Understanding these features is the basis for you to manage accounts.

Some account features help you identify accounts and the files and resources associated with them. Knowing how to use these features will help you track down account-related problems and manage the computer's users.

> Even a single-user workstation uses multi-ple accounts. Such a computer may have just one user account, but several system accounts to help keep the computer running.