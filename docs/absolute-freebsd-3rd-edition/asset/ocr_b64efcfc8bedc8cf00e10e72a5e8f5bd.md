# /etc/mail

Most of the contents of `/etc/mail` are dedicated to Sendmail. The two exceptions are the aliases(5) file and mailer.conf(5). We discuss both in Chapter 20.

# /etc/mail.rc

While FreeBSD uses most .rc files for system startup, the `/etc/mail.rc` file is used to configure mail(1).

# /etc/mail/mailer.conf

FreeBSD allows you to choose any mail server program you like via `/etc/mail/mailer.conf`, as covered in Chapter 20.

# /etc/make.conf

To make, or compile, a program is to build it from source code into machine language. We’ll discuss building software in detail in Chapter 17. The `/etc/make.conf` contains settings that control how the building process works, letting you set options that directly affect software builds. Remember, anything you add to make.conf affects all software built on the system, including system upgrades. This may cause upgrade failures. Many of the options from make.conf are useful only to developers.

If you’re interested in setting options that affect only system upgrades, use `/etc/src.conf` instead.

Here are some common features set in make.conf. Any values set here require the same syntax used by make(1). If you insist on trying to optimize software builds, follow the examples in make.conf(5) or in the software’s documentation. Best of all, though, don’t muck with make at all.