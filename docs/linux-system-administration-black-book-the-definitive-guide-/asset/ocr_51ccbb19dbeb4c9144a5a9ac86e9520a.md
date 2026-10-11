# In Depth

Email is possibly the most popular service on the Internet. It is also one of the most abused. It is important to understand how to set up a mail server so that it closely matches your needs but does not sit wide open for those people who might exploit it to bounce mass mailings off of. Setting up and running an email server has many other subtleties, so make sure to take the time to become thoroughly familiar with its inner workings.

# How Email Gets To Its Destination

The life of a piece of email begins when a user opens a new mail document in his or her mail client. This client, regardless of which it is, immediately asks for two pieces of information: the recipient’s email address, which is typically in the form *user@domain.extension* on the Internet, and the subject, which is as irrelevant to the email delivery process as is the mail’s content. However, some email clients will not even allow you to send an email message without some kind of subject in place.

# How Email Travels

After the user finishes writing an email, he or she clicks or presses whatever is necessary to send it off into the digital world. The client hands the mail off to the local Mail Transfer Agent (MTA). If the mail is destined for another user on this same machine, the local mail handler (**procmail**, in this case, but often `/bin/mail`) takes care of it. However, if the mail is meant for another machine—whether on your network or elsewhere on the Internet—the mail is passed on to a **sendmail** server. This server first determines whether the piece of email is meant for someone locally, in which case it delivers it.

If the mail is meant for someone on the Internet, **sendmail** uses your resolver to contact the zone server for the destination’s domain extension. That zone server tells your system who runs name service for the particular domain. The resolver then contacts the local name server for its MX record to find out which machine at that domain is the primary mail server. The **sendmail** server then sends the piece of email, using the Simple Mail Transfer Prototol (SMTP), to the mail server listed in the MX record.

The recipient’s mail server receives the mail through SMTP and analyzes the header information through its own rules. If all is well, the mail is delivered to the