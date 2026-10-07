A similar tool exists for Yahoo! FetchYahoo is available from
http://web.mit.edu/ravir/fetchyahoo/index.html.

Once implemented, you can use a regular MUA, or mail client, like the ones discussed
next, to access your Web-based mail.

# Mail Daemons

Red Hat provides a package named imam that will install IMAP and POP daemons (servers)
for your system. These servers receive mail from a remote site. Once installed (using the
pm command or through the Packages graphical interface—see Chapter 8), the document-
tation will be found in /usr/share/doc/imap-201a and the README is brief; Red Hat hasnalready done the configuration for: You only need to start the services (see Chapter 7).

Biff and its KDE Korn are small daemons that monitor your mail folder and notify
when a message has been placed. These are installed by default. It is common to
biff y in the .login or .profile files to automatically start it upon user login
to use Biff. Korn can be started by adding the app to the KDE taskbar.

> NOTE
Autoresponders automatically generate replies to received messages; they're commonly used to
otify others that the recipient is out of the office. Red Hat does not include one, but you can
find and install an autresponder at Freshmail.net. If you are subscribed to a mailing list, be
aware that automatic responses from your account can be varying to others on the list.
nPlease unsubscribe from mail lists before you leave the office with your autresponder activated.

# Choosing a Mail Client (MUA)

You use a mail client to read your mail. Several console mail clients are available for Red
Hat. These include highly configurable command-line clients and easy-to-use
menu driven clients. The following sections discuss a few of these, finally exam-
ing GUI mail client programs because they are the MUAs most chosen by new
users. Many people find the text MUAs useful once they try them, however, so don't cheat
yourself and overlook them.

The graphical MUA you choose will most likely bear resemblance to the Microsoft
Outlook or Outlook Express mail clients. Those applications are in widespread use
to many users. The modern Linux GUI mail clients build on that family-
arity providing enhancements, functionality, and configurability that are the hall-
marks of the UNIX environment.

# The mail Application

A UNIX utility named mail is included with all UNIX and Linux distributions. Because it
has a very Spartan interface, it's not used interactively. However, it is still an