
## Can you give me an example of how "power users" edit the default keytables?

A popular thing to do among "power users" is to swap the CAPS LOCK and CTRL modifiers around so that pressing the CAPS LOCK key gives you a control sequence. If you do a lot of switching back and forth between a "real" UNIX keyboard and a PC keyboard, you may find it useful to do this too.

## How do keytables really work?

OK, by now the smart ones among you are thinking "but wait, what about all those other weird entries I see in the table?" What you're referring to are entries that look a little more complicated, like this one:

```
keycode  2 = one
shift    keycode  2 = exclam
alt      keycode  2 = Meta_one
alt shift keycode  2 = Meta_exclam
```

Let's demystify these while we're at it. The extra fields here are just codes for when certain modifier keys are pressed with the key in question. For example, pressing the key labeled 1 on your keyboard doesn't really generate a "1." It generates a keycode of 2. Don't get confused, this is just the lookup code, remember? Now, if you pressed this key alone (without pressing SHIFT, CTRL, or ESC), the kernel would look up code number 2 in the list, map it to the "1" entry, and promptly spit out a "1" on your display. What happens when you press SHIFT-1 though? The kernel goes "Hmm... there's a SHIFT key with this one, so I need to use the SHIFT modifier, which is the second field" and you get a ! symbol (a "bang" in UNIX parlance). There are also other entries for other states that a key can be in. If you mess around with these, be careful, because you can really hose your keyboard—to the point that a reboot won't help at all.

## What are "meta" keys?

Another confusing point that often arises around UNIX keyboards is when people refer to "meta" keys. If you're an emacs user you are probably quite used to seeing meta sequences. Even if you're not an emacs user, you've probably

heard the term before. Well, to make a long story short, there's really no magic involved with the meta key. It's just another modifier key like the CTRL key. However, most PC keyboards don't have a key labeled META. Most well-written UNIX applications take this into account and allow you to simulate a meta sequence by pressing and releasing the ESC key to simulate pressing a META key. If you want a real live permanent META key, though, you'll have to edit your keytables and swap around some key functions.

Personally, we find the CAPS LOCK key rather annoying, so we usually end up mapping it to CTRL and mapping the left-hand CTRL key to a META key. We do this in console mode by editing the keytables. We have to do it again in a different way when we're in graphical mode, since key mappings don't get carried over automatically. In graphical mode there's nothing magic about Linux, though, and you can use any of the standard UNIX hacks to map your keyboard around enough to confuse anyone in your workgroup. We'll revisit this issue again when we talk about X Windows, just to keep it fresh in your mind.

## PASSWORD SECURITY

What can you tell me about Linux and password security?

One place where Linux differs noticeably from some of the commercial versions of UNIX is in the area of password security. Out of the box, Linux does not come configured with so-called shadow passwords. Shadow passwords are something you really shouldn't have to worry about unless you're a system administrator, but if you do happen to be your own system administrator and you want to increase the security of your system, you might want to consider upgrading. Most of the common FTP sites will have suites of precompiled programs to enable shadow passwords, and if you're a Redhat user you can download rpm packages and upgrade on the fly.

Even though most of the distributions don't come with shadow passwords enabled by default, the Redhat distribution has definitely beaten several of the commercial UNIX variants to the punch by including a little add-on called
