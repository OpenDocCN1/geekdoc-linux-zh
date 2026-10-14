Smileys (sometimes called emoticons), or textual representations of emotions that people commonly use in their email, are one way to express feelings in the otherwise emotionless world of email. When you see a collection of dashes, parentheses, and other punctuation marks (like :-) or :-(for example) that don’t seem to make sense, try turning your head sideways, and the meaning should come into focus right away.

One final point on netiquette, DON’T SHOUT! Even though email addresses are not case sensitive, the people who read email often are. And the use of ALL CAPITAL LETTERS in email is considered shouting. It’ll also brand you (deservedly or not) as a clueless newbie who can’t find the right key to turn off the caps.

# Sending Email with Linux

The most basic way to send email on a Linux system is with the mail command. The mail program is a command-line interface for sending and receiving electronic mail. It works, but it’s not pretty. Later in this chapter, you’ll learn about Pine, a much friendlier email interface, but you should know how to use mail since it’s guaranteed to be available on any Unix system.

Let’s say you’re logged in as root and you want to send a message to hermie. Start the process by typing

```
mail hermie
```

The system will respond with a “Subject:” prompt. Type the subject for your note, press ENTER, and then write your message, line by line. When you’re done with your missive, press ENTER to get to a blank line, then CTRL-D to send it.

Here’s a sample mail session. (The stuff you type is shown in bold, and the system prompts are normal intensity.)

```
# mail hermie
Subject: Gone Fishing
I’ve decided to kick back this afternoon and go fishing.
So if this crazy Linux system rolls over and dies,
I suggest you do likewise.
^D
EOT
```