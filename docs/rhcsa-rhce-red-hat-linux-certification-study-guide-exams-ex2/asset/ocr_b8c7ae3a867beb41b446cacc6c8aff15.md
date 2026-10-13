8. In what directory can you find documentation associated with the Postfix server?

# The Other SMTP Service: sendmail

9. In what file would you store forwarding e-mail addresses?

10. Why would you want to comment out the following directive in sendmail.mc?

```
DAEMON_OPTIONS(`Port=smtp,Addr=127.0.0.1, Name=MTA')dnl
```

11. What do you need if you want to comment out the following directive in sendmail.mc?

```
FEATURE(`accept_unresolvable_domains')dnl
```

12. What command processes all files in /etc/mail?

# LAB QUESTIONS

Several of these labs involve configuration exercises. You should do these exercises on test machines only. It's assumed that you're running these exercises on virtual machines such as KVM. For this chapter, it's also assumed that you may be changing the configuration of a physical host system for such virtual machines.

Red Hat presents its exams electronically. For that reason, the labs in this and future chapters are available from the CD that accompanies the book, in the Chapter13/ subdirectory. In case you haven't yet set up RHEL 6 on a system, refer to Chapter 1 for installation instructions.

The answers for each lab follow the Self Test answers for the fill-in-the-blank questions.