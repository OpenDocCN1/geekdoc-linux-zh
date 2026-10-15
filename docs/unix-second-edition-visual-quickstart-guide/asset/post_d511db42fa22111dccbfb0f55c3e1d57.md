
## Announcing an Absence with vacation

If you’re planning a vacation and will be away from your email for a while, let Unix announce your absence for you (Figure 11.15). Using the vacation program, you can have Unix send a reply saying that you’re out of the office to everyone who sends you email.

Keep in mind that vacation is quite variable among different Unix systems and ISPs. What you have might be different from the “standard” form used here. Be sure to check with your system administrator for specific instructions if you have any problems, and also look at the procmail section of this chapter, as many newer Linux and Unix systems use procmail instead of a .forward file to tell vacation to respond to your messages.

### To send “I’m on vacation” messages using vacation:

1. `vi ~/vacation.msg`

   At the shell prompt, type `vi ~/vacation.msg`. You’ll need to edit a message (a template, actually) for the vacation that people should receive when they email you, as shown in Figure 11.15.

2. `Subject: away from my mail!`

   Thanks for emailing me about $SUBJECT. Fortunately for me, I’m taking a fabulous vacation mowing my lawn, doing laundry, and catching up on other things I can’t do because I usually work so much. If you would like me to stay on vacation, please email my boss (boss@example.com) and let her know. Thanks!

   Create and edit the text to say what you want.

   The $SUBJECT term in the text will be replaced with the actual subject of the email sent to you.

![](img/6ffd6bb320ccf354f5a4d57c9d95190d_256_0.png)

3. Save your text and exit the editor.

   Chapter 4 has the gory details about saving and exiting in pico and vi.

4. `vacation -I`

   Type `vacation -I` at the shell prompt to start vacation and tell it to respond to all incoming messages. You'll still get the incoming messages in your in-box. In fact, they'll pile up in your in-box and wait for you to return.

5. `cat ~/.forward`

   Look at the .forward file in your home directory to verify that it contains a reference to the vacation program. Your .forward file specifies what should happen to your mail upon receipt. In this example, it should be processed by vacation. The reference to vacation is usually automatically inserted by the vacation program, but if it's not there, you'll need to edit the .forward file and add text like `yourid, "|vacation yourid"`. Of course, substitute your real userid for the placeholder above, and possibly include the full path to vacation (`/usr/bin/vacation` on our system). (See Code Listing 11.6.)

   Code Listing 11.6 Your .forward file should reference the vacation file.

   ```
   [ejr@hobbes ejr]$ cat ~/.forward
   ejr, "|vacation ejr"
   [ejr@hobbes ejr]$
   ```

### Tip

- Remember to unsubscribe to all mailing lists before you start vacation. If you don't, you'll send a vacation announcement to a whole list of people who likely don't care (not to mention that you'll really irritate the list administrator!). Or, worse, you might cause a mail loop (in which your messages to the list are acknowledged by the server, and the acknowledgements are in turn sent vacation announcements), causing hundreds or thousands of messages to accumulate in your account. It shouldn't happen, but it sometimes does.

### To stop vacation emails:

- `mv .forward vacation-forward`

At the shell prompt, move the .forward file that references the vacation program to a different name (in this case, vacation-forward). You could just delete it or remove the reference to vacation, but it's easier to save it so you can reuse it for your next vacation.

## Configuring procmail

Let's see...two messages from the boss...17 messages from the string collector's discussion group...oh, hey, a message from mom...and...

One of the handiest things you can do to make your Unix life easier is to use procmail (a mail-filtering program) to automatically handle some of your incoming email.

In this section, we'll show you how to configure procmail so you can manage incoming messages. As Figures 11.16 and 11.17 show, you need to do two things to set up your system to manage mail with procmail:

- Specify settings for procmail (Figure 11.16). For example, incoming mail normally gets plunked directly into your in-box; however, procmail filters mail before it even gets to your in-box, so you need to tell procmail where your mail folders are, among other things.

- Tell procmail to do its thing (Figure 11.17). Essentially, you create a .forward file that sends your incoming mail to procmail for processing before you ever see it. This step is not necessary for many systems, particularly newer Linux and Unix systems.

### To specify settings for procmail:

1. `pico ~/.procmailrc`

   To begin, access your editor and create a `.procmailrc` file in your home directory.

2. `LOGFILE=$HOME/.mailog`

   Give procmail a place to log all of its activities, so it can tell you what it's done: "I threw away 7 messages from your boss... filed 3 messages from Joe in the GolfBuddies folder..." In this example, we tell procmail to keep a log file called `.mailog` in our home directory (Figure 11.16). Keep an eye on this file, because it can grow large over time.

![](img/6ffd6bb320ccf354f5a4d57c9d95190d_258_0.png)

![](img/6ffd6bb320ccf354f5a4d57c9d95190d_258_1.png)
