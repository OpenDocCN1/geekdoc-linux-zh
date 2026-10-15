
## 6. Esc

When you're finished, press Esc (to get into command mode).

## 7. :wq

Then type :wq to save your work and exit the editor.

## 8. Y

Press Y to send the message. If you decide you don't want to share details about your belly button after all, you can press E to edit your message or press Q to quit and forget the whole thing.

## ✓ Tips

- You can change the default editor from vi to something else available on your Unix system. All you have to do is edit your ~/.muttrc file (or create one if it doesn't exist) and add set editor="emacs" (or whatever editor) to the file. See Chapter 8 for more information about changing variables.
- To send a quick message from the shell prompt, type mutt followed by the recipient's email address, as in mutt winchester@roycomm.com. If you want to send email to multiple addresses, just separate them with commas or spaces, as in mutt unixvgs@roycomm.com, info@roycomm.com.

## Reading Email with mail

In general, using mail is a bit less intuitive than using either pine or mutt; however, reading email with mail is particularly—um—challenging. Although we’d recommend using another program to read email if at all possible, here are the steps for reading email with mail if you’re daring enough or if you have no other options. Figure 11.12 illustrates this fairly quick task.

![](img/6ffd6bb320ccf354f5a4d57c9d95190d_250_0.png)

Figure 11.12 The mail screen is anything but intuitive, but you can see the messages you have.

## To read email with mail:

- 1. mail
  Type mail at the shell prompt. You’ll get a list of messages and a prompt (Figure 11.12).
- 2. 3
  Type the number of the message you want to read and press Enter.
- 3. Marvelous...he’s such a jerk...oh, that’s neat....
  Read your messages. Press N to move to the next message, or more to page through the message a screen at a time.
- 4. Q
  Press Q to quit mail when you’re ready.

## ✓ Tips

- If somebody really long-winded sends you a long message, your Unix system might just zip the message on by, leaving you reading only the bottom few lines. To read the message in its entirety, either type more to page through the message, or type s followed by the message number to save it to a file, and then use the editor of your choice read it.
- Type h followed by a message number to see different message headers. For example, type h 117 to see the messages leading up to number 117.
- Find a different mail program if at all possible—it’s useful to be able to cope with mail for times of need, but it’s not a good long-term solution.

## Sending Email with mail

Despite mail’s unintuitive interface and features, it is a great program to use if you just want to dash off a quick message without fussing with niceties. As Code Listing 11.3 shows, you can send messages while in mail or from the shell prompt. You can also use mail to send files fairly easily.

## To compose and send a message using mail:

- 1. mail unixvqs@raycomm.com
  At the shell prompt, type mail followed by the recipient’s address. If you want to send email to multiple addresses, just separate them with commas but no spaces, as in mail putz@raycomm.com,putz2@raycomm.com. If you’re already in mail, just type m followed by the address or addresses, like m putz@raycomm.com,deb@roycomm.com.
- 2. So, anyway, Winchester had perched himself on my stereo turntable (those were sooooo low-tech, weren’t they?!). He was waiting for me to turn on the stereo so he could go back to sleep while spinning in circles. I used to let him sleep that way at night. Well, that was until one night the lid closed on him…
  Type in your message text (see Code Listing 11.3).
- 3. Ctrl D
  Announce that you’re done with either a . (dot) by itself on the last line or with Ctrl D, and the message will zip off to the recipient(s).

```
[ejr@Hobbes ejr]$ mail debroy
Subject: You’re in big trouble now!
So, anyway, Winchester had perched himself on my stereo turntable (those were sooooo low-tech, weren’t they?!). He was waiting for me to turn on the stereo so he could go back to sleep while spinning in circles. I used to let him sleep that way at night. Well, that was until one night when the lid closed on him…
EOT
[ejr@Hobbes ejr]$
```

Code Listing 11.3 Using mail, you can dash off a quick note by including the recipient’s address and the message text.
