# # Chapter 4: Serving Up Mail and News

*In This Chapter*

+   - Installing and using `sendmail`
+   - Testing mail delivery manually
+   - Configuring `sendmail`
+   - Installing the InterNetNews (INN) server
+   - Configuring and starting INN
+   - Setting up local newsgroups

Electronic mail (e-mail) is one of the popular services available on Internet hosts. E-mail software comes in two parts: a mail-transport agent (MTA), which physically sends and receives mail messages; and a mail-user agent (MUA), which reads messages and prepares new messages. In this chapter, I describe the e-mail service and show you how to configure the `sendmail` server on a Fedora Core PC.

Internet newsgroups provide another convenient way, besides e-mail, to discuss various topics and to share your knowledge with others. Fedora Core comes with the software you need to read newsgroups and to set up your own system as a news server. In this chapter, I describe how to configure and run the InterNetNews server, a popular news server. I also show you how to set up local newsgroups for your corporate intranet (or even your home network).

# ## Installing the Mail Server

If you install the mail server software during Fedora Core installation, you don't have to do much more to begin using the mail service. To see whether the mail server is already installed, type the following command:

```
```bash
rpm -q sendmail
```
```