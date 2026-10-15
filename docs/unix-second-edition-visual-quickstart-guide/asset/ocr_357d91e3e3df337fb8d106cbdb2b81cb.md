# Sending Email with mail

Despite mail’s unintuitive interface and features, it is a great program to use if you just want to dash off a quick message without fussing with niceties. As Code Listing 11.3 shows, you can send messages while in mail or from the shell prompt. You can also use mail to send files fairly easily.

# To compose and send a message using mail:

+   1. mail unixvqs@raycomm.com
+   At the shell prompt, type mail followed by the recipient’s address. If you want to send email to multiple addresses, just separate them with commas but no spaces, as in mail putz@raycomm.com,putz2@raycomm.com. If you’re already in mail, just type m followed by the address or addresses, like m putz@raycomm.com,deb@raycomm.com.

+   2. So, anyway, Winchester had perched himself on my stereo turntable (those were sooooo low-tech, weren’t they?!). He was waiting for me to turn on the stereo so he could go back to sleep while spinning in circles. I used to let him sleep that way at night. Well, that was until one night the lid closed on him…
+   Type in your message text (see Code Listing 11.3).

+   3. Ctrl D
+   Announce that you’re done with either a . (dot) by itself on the last line or with Ctrl D, and the message will zip off to the recipient(s).

```
[ejr@Hobbes ejr]$ mail debroy
Subject: You’re in big trouble now!
So, anyway, Winchester had perched himself on my stereo turntable (those were sooooo low-tech, weren’t they?!). He was waiting for me to turn on the stereo so he could go back to sleep while spinning in circles. I used to let him sleep that way at night. Well, that was until one night when the lid closed on him…
EOT
[ejr@Hobbes ejr]$
```

Code Listing 11.3 Using mail, you can dash off a quick note by including the recipient’s address and the message text.