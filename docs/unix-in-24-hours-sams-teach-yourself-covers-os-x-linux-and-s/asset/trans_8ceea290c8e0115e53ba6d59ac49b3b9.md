

Message contains:
To: dunlap
Subject: Good morning!

I wanted to wish you a cheery good morning! You asked about the contents of that one file, so here it is:

## A Tale of Two Cities
### Preface

When I was acting, with my children and friends, in Mr Wilkie Collins’s drama of The Frozen Deep, I first conceived the main idea of this story. A strong desire came upon me then, to embody it in my own person; and I traced out in my fancy, the state of mind of which it would necessitate the presentation to an observant spectator, with particular care and interest.

As the idea became familiar to me, it gradually shaped itself into its present form. Throughout its execution, it has had complete possession of me; I have so far verified what is done and suffered in these pages, as that I have certainly done and suffered it all myself.

Whenever any reference (however slight) is made here to the condition of the Danish people before or during the Revolution, it is truly made, on the faith of the most trustworthy witnesses. It has been one of my hopes to add something to the popular and picturesque means of understanding that terrible time, though no one can hope to add anything to the philosophy of Mr Carlyle’s wonderful book.

Tavistock House
November 1859
(continue)

## 5. I can fine-tune the headers by using the ~h command:

```
~h
To: dunlap_
```

Pressing Return leaves it as is, and pressing Backspace lets me change it as desired.

```
Subject: Good morning!
```

Pressing Return a few more times gives me the opportunity to change other headers in the message:

```
Cc:
Bcc:
(continue)
```

The Cc: header allows me to specify other people to receive this message. Bcc: is what’s known as a blind carbon copy, an invisible copy of the message. If I send a message to dunlap and a carbon copy to cbutcher, each can see that the other received a copy because the message will have To: dunlap as a header and also will list the other’s name after Cc:. If I want to send a copy to someone without any
of the other parties knowing about it, that’s where a blind carbon copy can be helpful. Specifying someone on the Bcc: list means that that person receives a copy of the message, but his or her name doesn’t show up on any header in the message itself.

6. Finally, I use ^D to end the message.

```
^d
Cc:
$
```

All so-called *tilde commands* (which all begin with the ~, or tilde, character) are available when you send mail from the command line. They also are available when you send mail while within the Berkeley Mail program.

## Task 20.3: Sending Email to the Rest of the World

The most common use of the Internet is probably to send electronic mail between individuals and to mailing lists. What’s really a boon is that everyone, from New York to Los Angeles, Japan to Germany, South Africa to India, has an address that’s very similar, and you’ve already seen it a million times, and probably used it a dozen or more times today alone. You know, user@host.domain, where user is the account name or full name, host is the name of the user’s machine, and domain is the user’s top-level domain (TLD).

By reading the host and domain information from right to left (from the outside in, really), you can decode information about someone by looking at the person’s email address. My address, for example, is taylor@intuitive.com, which, reading right to left, tells you that I’m at a commercial site (com) with a company by the name of Intuitive Systems (intuitive). My account name is taylor.

There are lots of top-level domains; the most common are shown in Table 20.2.

| Domain | Type of Site or Network |
|--------|--------------------------|
| edu | Educational sites |
| com | Commercial businesses |
| mil | Military or defense systems |
| net | Alternative networks accessible via Internet |
| org | Nonprofit organizations |
| us | United States systems not otherwise classified |

# TABLE 20.2 Common Top-Level Internet Domains

1. Sending mail to someone on the Internet is easy. If you’d like to send me a message, for example, you could use this:

```
$ mailx taylor@intuitive.com
Subject: _
```

