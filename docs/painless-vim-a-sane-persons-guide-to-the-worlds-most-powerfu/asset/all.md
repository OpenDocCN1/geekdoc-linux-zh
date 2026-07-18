![](images/title_page.png)

![Painless Vim](images/title_page.png)

## Painless Vim

### A Sane Person’s Guide to the World’s Most Powerful Editor

#### Nate Dickson

This book is for sale at [http://leanpub.com/painless_vim](http://leanpub.com/painless_vim)

This version was published on 2018-07-30

![publisher's logo](images/leanpub-logo.png)

*   *   *   *   *

This is a [Leanpub](http://leanpub.com) book. Leanpub empowers authors and publishers with the Lean Publishing process. [Lean Publishing](http://leanpub.com/manifesto) is the act of publishing an in-progress ebook using lightweight tools and many iterations to get reader feedback, pivot until you have the right book and build traction once you do.

*   *   *   *   *

© 2013 - 2018 Nate Dickson

## Table of Contents

## Guide

1.  [Begin Reading](#chap00.xhtml)

## Preface

### Why? Why This?

Look, we’ve all been through this: someone says, “You should learn vim. I did, and now I’m 10000% faster at everything and people like me more.” So you download the latest version for your OS and start it up and, hey look, there’s that screen with a bunch of tildes down the side asking you to donate to kids in Uganda. Just like the last time you tried this. You know from experience that typing `:help` isn’t going to be super helpful, because you’ll get stuck in the help window and you’ll never be able to get it to go away. You start typing and the terminal beeps at you or says it’s in some weird mode now or –if you’re lucky– starts putting letters on the screen at some point. Then it’s a quick trip to Google to figure out how to get back *out* of Vim, and you shudder, vowing not to go back.

It doesn’t have to be this way.

At its heart, Vim is about making life easier for developers. But most of the “beginners” advice you get sounds like there’s a big trial by fire initiation that you have to pass before you can get to that programmer’s nirvana. People tell you that the “only way” you’ll ever get good at using the power of vim is to throw your mouse out the window, disable all the hotkeys you’re used to, and just spend a few months doing nothing but learning how to use an editor.

Bless their pointy little heads. It’s true that once you’re *good* at vim you will start to see all the system shortcuts and mouse shortcuts as inefficient. But when you’re starting out they make it feel like you’re suddenly in a foreign country where you don’t speak the language. They mean well, but that sort of initiation is exactly wrong for a newcomer. It’s advice like that that is impeding vim, keeping it from being *the* editor that everyone uses^([1](#chap35.xhtml_fn-Katz)) .

### I’m a Stranger Here, Myself

The fact is, you *can* learn vim at your own pace and be fairly productive with it right out of the box. And that’s what this book is about. If vim were a foreign country, I would be the guy who walks up to you in the hotel lobby and says, “Hey, how’s it going? Just get here? I’m a stranger here myself.” And then I would show you all the good restaurants and stuff, because I understand what you’re going through.

So instead of lecturing you on learning all the underlying `ex` and `vi` commands that you “have to know to *truly* experience the *raw power* of vim” I’m going to show you how to get in, get comfortable, and start branching out into bigger and better things. I’m going to take it as read that you’re not 100% committed to leaving all other text editors behind. Heck, I’d strongly suggest having a copy of Sublime Text (more on that later) available for the times where you’re just sick to the eye teeth of vim. It happens! But come back to vim, because I plan to show you that vim isn’t that hard, and that learning it can be *painless*.

## Introduction

### Why Learn Vim

Vim, for all its eccentricities, is designed to be *fast* and *developer friendly*. Smart people have been using and improving it for decades and it’s gotten to the point that it’s pretty darn good in the right hands. As a former vim critic who has started using it, I can tell you that it is *that* fast when you get going. You can make a surprising number of changes quickly and efficiently in vim, and once you start navigating, making changes, and issuing commands using just the home row keys using anything else will feel clunky by comparison.

#### It is *that* fast

Vim, used well, is a speed *demon*. Once you get used to the slightly weird controls every other text editor will feel unwieldy. Vim was designed to keep your hands where they belong, without using the mouse or the arrow keys.

Now, like I said before, if you want to use the mouse and arrow keys while you get used to vim, go right ahead! You’re not being productive if all you’re doing is trying to remember how to edit the third character in the line below your cursor. But the *promise* is that eventually you’ll get comfortable with the vim way of doing things and be much happier. There are other reasons, too:

#### Vim *commands* get around

A lot of unix-y things use the vim keybindings for moving around. Even web services like gmail use the `h j k l` magic keys to move between emails. If you get comfortable with vim idioms you’ll be more comfortable with a lot of other tools as well.

#### Vim *itself* gets around

Let’s face it, vim is *everywhere*. If you install git on windows vim comes along for the ride. If you have a Linux box or a Mac you’ve already got vim. And if you’re like me^([2](#chap35.xhtml_fn-1)) it’s always slightly bugged you that there was this editor on your machine that you don’t like or know how to use. If you get comfortable with vim then you don’t have to panic when you have to enter a commit message from the command line in git.

### What This Book Is

This book aims to be:

#### Short

You’ve got better things to do than read books about editors. The main goal of this book is to get you comfortable with the editor and feeling like you’re ready to move on, bending vim to your wishes. If you’re like me, you get annoyed at making changes someone else forced on you after a while, and you just want to strike out and do it yourself. I’ll let you do just that.

#### Cheap

Vim is free. While I don’t want to sell my work for nothing, I’m coming pretty darn close. This is a beginner’s book, and my goal is to lower the bar to entry. To start with, I’ll price it low and hope that helps you along.

#### Easy to understand

Vim is complex; this book shouldn’t be. My main goal here is to help you build confidence and get your feet under you. If you’re reading this during the beta period and you’ve got suggestions, please send them on over to me! I’m more than willing to listen and change.

#### Friendly!

My high horse died a while back, and I never bothered to buy myself a soapbox, so I won’t be doing any preaching. Remember that friendly face in the hotel who shows you all the great spots in town? That’s this book. I’m not here to judge.

#### Opinionated (but in a good way)

I’ll keep the tone friendly, but I got *opinions* people. There are things I think are good and things I think aren’t so good. But I’ll let you know *why* I think some things are good or not so good and let you make up your mind on your own.

#### Lighthearted, but serious

The *tone* of the book is meant to be light and approachable, but the *advice* is meant to be rock solid. I’m not going to have you do things to your configuration files that I wouldn’t do, even temporarily, or to prove a point. The goal is to make it easy for you to get things *right* ^([3](#chap35.xhtml_fn-2)) the first time.

### What This Book Isn’t

This book definitely is *not*:

#### The end-all-be-all reference on vim

I’m here to help you get started, not to be the only book you’ll ever buy on the subject. The main reason for this isn’t laziness, thank you very much. Well, okay, it kind of is. There are a *ton* of books, websites, wikis, and other documentation out there that will help you along, once you get over the initial learning curve. I’m here to help you over that first curve.

#### A list of tips

A lot of the stuff in the later chapters won’t make a ton of sense if you haven’t been through the earlier chapters. The chapters are laid out iteratively, starting with small changes that build up to a final configuration that should work well. Then you’ll have a good jumping-off point for your further modifications.

#### A deep dive

The goal here is to give you enough information to be comfortable, but not all the underlying technologies and line editor commands and other such things. Again, these are available online and in many other reference guides all over the place. When you decide that you want to know more about something you’ll be able to find it. I have faith in you.

### Who am I?

I’m Nate Dickson, it says so right on the cover.

But beyond that, I’m a professional programmer by day, blogger, writer, and daddy by night. You can check out a fairly large amount of my writing on my personal blog^([4](#chap35.xhtml_fn-3)), or my less-maintained Apple blog^([5](#chap35.xhtml_fn-4)). You can also check me out on Twitter^([6](#chap35.xhtml_fn-6)), or Github^([7](#chap35.xhtml_fn-7)).

In terms of my vim credentials, I don’t have many. I use vim in my day job and I’m a command line junky, with the `.zshrc` and `.tmux.conf` files to prove it.

But my quasi newbie status is part of why I’m writing this book right now. I’ve spent the last few months combing blogs and websites, buying or borrowing books on vim and grabbing onto the arm of anyone I know who uses vim and begging them to help me fix whatever mess I’ve most recently gotten myself into. Now that I’m fairly comfortable, I’d like to pass what I’ve learned along to ease the learning curve for everyone else.

### References

I will refer you to a lot of other books, posters, blogs, wikis, etc. etc. over the course of this book. For the most part these are things I’ve used extensively myself, and can heartily recommend. Again, I’ll try to provide reasons for my references and let you decide if it sounds like something you’d like to investigate on your own.

### Sample Documents

Throughout the book there will be exercises to try out. For convenience, I have created a repository of sample documents for use with these exercises. They are stored on [Github](https://github.com/PogiNate/Painless-Vim-Samples), and the readme file has instructions for how to get them in place, if you’re not familiar with git and Github.

### The Obligatory “Conventions Used in This Book” Section

First off, regarding the actual word “vim”. In general I will write it all lowercase, because that’s how most people think of it, like “perl” or “ruby”. That’s the command you enter to start the editor, and that’s really the name of the program.

However, when it’s in a book, chapter, or section title I will capitalize it, just as I would any other word in a title: *Painless Vim*

Ironically, even though it’s probably the most correct, I will never write it as “VIM”, even though it is a acronym (kinda) for “Vi IMproved”

Other than that, I use the same conventions everyone else uses. Code appears in `a monospaced font`, and longer blocks of code will appear

```
1 in a large block
2 of monospaced text.
```

Special keys like `<shift>`, `<enter>`, `<esc`>, will have angle brackets around the name to make it real obvious that you shouldn’t be typing that word, you should be pressing that key. If you need to press `<ctrl>` and another key at the same time (and you *will* need to do this, quite frequently) I’ll just write them like so: `<ctrl>d`.

Vim uses both upper- and lower-case characters, so remember that “`S`” is `<shift>s` and “s” is just `s`.

Those are the only two times you should ever need to press two keys at the same time: either to hit `<ctrl>` and a character, or to press `<shift>` and a character to make something upper-case.

Which is good, because there will be a lot of times where you have to hit multiple characters in sequence. For example, let’s say you need to delete the next character after your cursor. You would press `d` (for delete) and then `l` (for the next character. Don’t worry about it now; we’ll get into it later). When I write this out in the book I will just write the two letters in a row, like so :

```
1 dl
```

I realize that looks exactly the same as my “type them at the same time” notation. Just remember that you’ll only ever need to press `<ctrl>` or `<shift>` at the same time as another character. In all other situations, two characters in sequence means type them one after the other.

Okay, got it? It’s pretty natural, I promise. Let’s move on.

From time to time I will need to show you *exactly* where your cursor needs to be when you perform a command. In these cases I will put a pipe symbol where the cursor resides, like so:

```
1 The cursor is in the middle of the word pi|pe
```

Again, this will all make more sense in a bit. For now let’s get moving.

## 1\. Get In, Get Out, Get Comfortable

Okay, you’ve gotten through the introduction. Good for you. I’d like to say that the style will settle down at this point, but I can’t promise that.

Here’s where we get started on the real meat of learning vim. We’re going to start simple: *open the editor*. For now I’d recommend doing things from the command line, not because I have some big problem with GUI’s, but because the graphical versions of vim tend to make little changes that can get in the way of the things we’re trying to do here. So, open a Terminal ^([8](#chap35.xhtml_fn-term)) and enter the following:

```
1 $ vim
```

![I have been here before. I don’t like it.](images/vim_intro.png)

I have been here before. I don’t like it.

There! That’s not so scary, is it? Just a bunch of tildes and some version information! Not scary at all!

Well, okay, yeah it is. You’re in this editor with no discernible way out. So let’s cut straight to the quick and talk about how to get back out. For now we’re going to use the absolute “oh crap let me out” method. Type `:q!<enter>`^([9](#chap35.xhtml_fn-out)) and you should be right back to the command prompt, which looks like this:

```
1 $
```

Okay, breathe. This time we’re going to go in armed a little better. Before you dive back in, find a file you’ve been working on lately. HTML files work well, but pretty much anything that is structured text or code will work just fine. If you don’t have anything that springs easily to mind you can use `sample.html` from my sample repository. Switch to the directory where that file is kept:

```
1 cd /path/to/where/the/file/lives
```

And do this:

```
1 vim file1.html
```

And you should see…a boring representation of your file. But we’re going to fix that right now. Enter the following:

```
1 :syntax on<enter>
```

And the file should brighten up a bit. We’ll talk more about colorful files in a bit, but for now let’s get back out of vim, because it’s still scary:

```
1 :q!<enter>
```

Okay, you’re safe. Let’s take a minute out here in the real world to formalize what we’ve just learned:

1.  When you start vim, the keyboard makes things happen instead of making letters appear.
2.  When you want to send a command to vim, you preface it with a colon (`:`).
3.  `:q!<enter>` gets you back out of vim without saving any changes.

Cool.

### Line numbers and Moving Around

All right, now that we’ve had a breather, let’s dive back into vim. Open your test file again with

```
1 $ vim file1.html
```

And you’ll see you’re right back to boring plain ol’ text. You can tell vim to color it again with

```
1 :syntax on<enter>
```

But it seems like a bummer to have to do this by hand every time you start vim. You’re right. Don’t worry, we’ll fix that.

But there’s more. We’ve learned that when you send commands to vim that start with a `:` you have to press `<enter>` at the end. This is useful information, because I’m going to stop putting `<enter>` after every command from here on out. Remember that if you start a vim command with a colon it always ends with an `<enter>`. There are other commands that *don’t* need an `<enter>` at the end. We’ll get to them in time. For now let’s look around this file.

## 2\. Moving Around in Vim: Baby Steps

Now that you’re in a file, it’s time to move around a little bit. If you’ve ever played with vim before, you’ve probably seen something that looks like this:

```
1 	k
2 h		l
3 	j
```

This is a super-unintuitive way of telling you which keys will move your cursor which directions. In English it goes like this:

*   `h` moves your cursor one space **left**
*   `l` moves your cursor one space **right**
*   `k` moves your cursor one line **up**
*   `j` moves your cursor one line **down**

So play with those four keys for a while. The layout is weird at first, I’ll grant you, but it serves the purpose of keeping your hand firmly on home row, and after a while you’ll start to just believe that `h j k l` should *always* move your cursor around. This is great when you’re using a program that understands vim keys. It also means that you’ll end up in an instant message conversation with someone, and you’ll inadvertently send them a message that says “jjjkl” as you try to figure out why you can’t move your cursor. It’s a curse.

Okay, moving on. Once you’ve gotten comfortable moving your cursor around, it’s time to *edit* something. Use the movement keys to get your cursor where you want it and press `i`.

At the bottom of the screen you should see a message appear:

```
1 --INSERT--
```

This is vim’s way of telling you that pressing keys now will make things change in your text. In vim parlance, you have just entered *insert mode*.

Type something witty in the document. I would put “So long, and thanks for all the fish” because it’s better than “hello world”. But I know it doesn’t matter what I tell you to enter; you’ll put whatever you want. That’s just how you are. You’re independent and I respect that.

Once your witticism is entered it’s time to save it up. Hit `<esc>` and the `--INSERT--` message at the bottom of the screen should disappear. This means that the keyboard is back to issuing commands to vim instead of changing the text on the screen. Vim calls this *normal mode*, but don’t worry too much about that yet. Type

```
1 :w
```

And your changes are *saved*, friend.^([10](#chap35.xhtml_fn-lastWarning))

Now let’s do something a little more daring and, dare I say it, *useful*. Moving around with your fingers on home row is nice and all, but it’s not worth all this hassle and bother. Let’s look at some slightly larger jumps in the text.

Position your cursor somewhere on a line of text–anywhere is fine– and make sure the `-- INSERT --` thingy is gone by pressing `<esc>` a bunch of times until vim starts beeping and/or flashing at you. ^([11](#chap35.xhtml_fn-Beep)) Now press `A`. Note that was an uppercase `A`, not a lowercase `a`. This handy little shortcut moves you to the end of the line and puts you back into insert mode, all at once. Think of it as “append” or “add”. Nifty, huh? Okay, press `<esc>` again and let’s do another one. Press `o`. (Again, note the case.) Vim adds an empty line, right under the line you were on, and once again you’re in Insert mode, ready to enter new text into the file. Write something if you want, and then press `<esc>` again to get out of Insert mode.

We’re going to talk more about moving the cursor around later, but for now look how awesome you already are! Since you don’t need to worry about changes this time, you can just type

```
1 :q!<enter>
```

To exit vim.

### Zoom!

Let’s go back into vim and play with three simple (but useful) commands that I call the *zoom* commands. To enter vim this time type

```
1 $ vim sample1.html
```

So that we’ve got a document to play with. Press `j` repeatedly to move your cursor down a few lines, it doesn’t matter where it ends up. What we’re going to do is tell vim to scroll the window so that the line the cursor is on is positioned where we want it.

The first “zoom” command is `zt`, which (I say) stands for “zoom top.” When you press `zt` in command mode it will move your current line to (you guessed it) the top of the screen. So, if your cursor is on line 15 and is one third of the way down the screen it will now be at the top of the screen.

Next up is `zb`, or “zoom bottom.” As you can guess, it moves your current line to the bottom of the screen, letting you see everything that came before.

The third and arguably most useful zoom command is `zz`, which positions the line your cursor is on in the *middle* of the screen, so that you can see that line in context. I use all three commands fairly frequently, but I find this is the one I like the best. It’s my secret favorite child.

All right, we’ve done some good work here. You’ve started vim and gotten around a bit, and more importantly, you made your code all pretty. In the next chapter we’ll get down to the single most important thing you ever have to do with an editor: choose your color scheme.

## 3\. Your `.vimrc` File And You

Okay, let me start by saying I didn’t lie to you. This chapter *is* about choosing a color scheme. But to do that we need to talk about how to save your settings from session to session. And the way to do this is through a `.vimrc` file.

For now, we’re going to start very *very* simply and just add a few lines. In general, any command that you can send to vim by typing `:` and then hitting enter can be put in your `.vimrc` file. We’re going to add two lines right now to solve a problem we had in the last chapter. Start by telling vim to open your `.vimrc` file. On a Unix-based machine it’s found at `~/.vimrc` ^([14](#chap35.xhtml_fn-WinVim))

From the command line open vim for editing with your `.vimrc` file as the subject:

```
1 $ vim ~/.vimrc
```

And, if you’re using a fresh install, you should see a completely empty file. Go into insert mode by pressing `i` and enter the following lines:

```
1 set nocompatible
2 syntax on
3 set nu
4 filetype indent plugin on
```

I realize this all looks like witchcraft at the moment, but it’s really just telling vim a few things about how you want it to behave. Let’s go through it line by line and you’ll see how simple it really is:

*   What’s that “nocompatible” thing? That line simply tells vim to be *vim* instead of being *vi*. It’s a good way to turn off all the old, weird, useless things that are holdovers from vim’s even older and more arcane predecessor. Just set that line and forget all about it. All it’s doing is protecting you.
*   ‘Syntax on` is what we’ve been talking about: this tells vim to do syntax highlighting. This is what turns on your pretty colors for good.
*   Okay, so, what about this `nu` thing? That tells vim to display line numbers down the left-hand side of the screen. You could (temporarily) do the same thing by typing `:nu` while in normal mode, but since vim is a programmer’s editor we’re going to make it a part of your everyday setup. If you hate line numbers you can omit it.
*   The last one…the last one is a bit magic. In a nutshell we’re telling vim to figure out what kind of file it’s looking at and load the appropriate filetype plugin. This has a lot of benefits for programmers^([15](#chap35.xhtml_fn-OrMarkdownUsers)), and even if you don’t fully understand it I would recommend setting it. Some of the great tricks you’ll learn later on in this book depend on it.

Press `<esc>` to get out of insert mode and save the file by typing

```
1 :w
```

So, now you have two choices. You can exit vim and start it again to have your changes take effect, or you can do some vim awesomeness. Instead of exiting vim, enter the following:

```
1 :so %
```

Now, before you close this book, feeling all hurt that I’m going to spring terrible surprises on you like `.vimrc` files and arcane `:so %` commands, hear me out. What you just did is tell vim to *source* ^([16](#chap35.xhtml_fn-read)) the current file. The `so` command is a shortcut for `source`, and `%` is a shortcut for “the current file”. See? Nothing scary happened here. This is a useful command to know while you’re getting your vim setup just right, and it makes you feel cool as well.

### I Was Promised Color Schemes!

Okay, look, all of this was just ground work we had to get through to get you your colors on a permanent basis. Adding a color scheme to vim is a two step process:

1.  Install a color scheme.
2.  Tell vim to use it.

And the easiest way to accomplish step 2 is in your `.vimrc` file.

#### Picking a Color Scheme

There are a ton of pre-built color schemes out there for vim. After all, people have been using it for more than 20 years, and everybody loves colors. There are many places to go to peruse available schemes and find one that fits your own personal style, a few of which are listed in [Appendix 1](#chap30.xhtml_color-schemes) .

For the purpose of this section, we’re going to install the [Tomorrow Theme](https://github.com/chriskempson/tomorrow-theme/tree/master/vim), because it comes with a few nice and elegant variations, and because it’s the one that I use right now. More specifically, I use “Tomorrow Night Eighties,” and therefore–at least for a little while–so will you. I’m all opinionated, remember?

So, to install the scheme, download the contents of the `colors` folder in the github repository. You should see a list of files, all of which have a `.vim` extension. Now it’s time to do some diving.

In your home directory there’s a hidden folder called `.vim`, which is where vim keeps all of its configuration stuff. Inside that directory is a folder called “colors,” and that’s where you want to put the color schemes you just downloaded. We’re going to discuss a better way to do this [soon](#chap11.xhtml_plugins), but for now just move those files from wherever you downloaded them to `~/.vim/colors`. On OSX I would do this:

```
1 $ mv ~/Downloads/colors/*.vim ~/.vim/colors
```

But however you get the files in place, you’ll want to end up in a situation where the output of `ls ~/.vim/colors` looks like this:

```
1 Tomorrow-Night-Blue.vim
2 Tomorrow-Night-Bright.vim 
3 Tomorrow-Night-Eighties.vim
4 Tomorrow.vim
```

You get the idea. Once that’s done it’s time to edit your `.vimrc` file some more. Open it up in vim and add this line:

```
1 colorscheme Tomorrow-Night-Eighties
```

And then hit `<esc>` to go back to normal mode. Save your work (`:w`), and then call on our old friend `:so %` to see your new color scheme in all its glory.

### Using Keymaps to Get Unlost

Let’s add one more line to your `.vimrc`, both as instruction and because it’s useful.

From time to time your cursor can get lost on screen. It’s nobody’s fault, screens these days are large and cursors are small. Therefore a lot of people like having their editor highlight the line where the cursor is sitting. Given vim’s line-editing abilities, this isn’t a terrible idea. There are definitely times where I want my cursor line highlighted, but not *all* the time. So let’s add a keymap to `.vimrc` that allows us to highlight and un-highlight the current line at will. Paste the following into your `.vimrc` file:

```
1 nnoremap <silent> <F4> :set cursorline!<CR>
```

The heart of this line is the command

```
1 `:set cursorline!`
```

All of that stuff before the command is simply a way to tell vim that we want it to do something when we press the `<F4>` key. Let’s examine the command in excruciating detail.

*   As we’ve learned before, if you type `:` at the beginning of something it tells vim that you’re sending it a command.
*   The `set` command tells vim that we’re going to, well, *set* an option. If we set things from the command line in vim it will be set for this session, if we set them in `.vimrc` they will be set for every vim session.
*   The `cursorline` option tells vim to highlight the line where the cursor is right now.
*   The `!` at the end of the option tells vim to toggle the `cursorline` option. If it’s currently on, turn it off and vice versa.
*   The `<CR>` at the end tells vim to simulate pressing the `<enter>` key. Remember, if a command begins with a colon it has to end with an `<enter>`.

## 4. Interlude: The Joy of a Good Cheat Sheet

While you’re learning vim it can be hard to remember all the commands and controls and letters and combinations and stuff, and sometimes no matter how much you ask your brain to pull up the one you need it’s just not going to do it.

Which is why it’s a good idea to have someone help you out. A simple memory prompt hung up on the wall behind your computer can spur your brain back into activity.

There are a lot of cheat sheets out there, most of which are the product of a lot of time and effort on the part of the creator, who was usually trying to create the “perfect” cheat sheet, meaning the one that works best for the way they think.

In fact, since I first wrote this “interlude” I have created my own cheat sheet, which is included in your *Painless Vim* download. And hey, you spent the money on a vim book, you deserve a cheat sheet to go along with it. My cheat sheet is a distillation of all the commands and actions that I find myself using most frequently.

But if you’re overburdened with cash, or just don’t particularly care for the *Painless Vim* cheat sheet then read on, my friend. I won’t be offended, I promise.

For my money ^([17](#chap35.xhtml_fn-money)) the best one out there is the [“Beautiful” Vim Cheat Sheet](http://vimcheatsheet.com/), because it’s clean, well laid out, and informative. When you start out you can just focus on the movement arrows that dominate the top left corner, and after a while you will start to see that the whole thing is packed with things you can use.

There are a number of [other good choices](#chap30.xhtml_cheat-sheets). The point of this interlude is to spend a little time finding one that makes sense to you. But the “Beautiful” one has earned itself a permanent spot on the wall behind my monitor. ^([18](#chap35.xhtml_fn-Until))

## 5. Moving Around in Vim: Grown Up Steps

Okay, now that the *serious business* of getting a color scheme set up is taken care of, let’s get back to moving around.

It’s often said that programming is roughly 90% thinking and 10% typing ^([19](#chap35.xhtml_fn-programmers)). While this may be true, I would add that a fair amount of time is also spent getting the cursor where you need it to be. Let’s say you made a change on line 15, and from there you need to move the end of the file to add a new method. In a regular editor you have a few choices: you can either press the down arrow a bunch of times, or take one hand off the keyboard entirely and click on the last line of the file. Vim has a better idea:

```
1 G
```

That’s it! Upper-case `G`, all by itself, will move your cursor to the last line of the file. Want to get back to the top of the file?

```
1 gg
```

And you’re there. The point is that moving around is supremely easy in vim, once you get the hang of it. So, let’s take a look at some of the most used *motions*^([20](#chap35.xhtml_fn-motions)) in vim:

simple motions

| Keystroke | Motion |
| --- | --- |
| h | move right |
| j | move down |
| k | move up |
| l | move left |
| b | previous word |
| e | end of word |
| ctrl+d | move down by 1/2 screen |
| ctrl+f | move down by 1 screen |
| ctrl+u | move up by 1/2 screen |
| ctrl+b | move up by 1 screen |
| gg | jump to the start of the file |
| G | jump to the end of the file |
| ^ | first non-whitespace character of the line |
| $ | last non-whitespace character of the line |
| `0` | beginning of the line |

There are quite a few more, but this will give us enough to get on with. Let’s play around with these actions for a moment. Open a file and jump around a bit, moving to the start and end of lines, bouncing around between words, etc.

The “screen” motions are a little harder to pin down, but once you get used to them they make sense. A “screen” consists of the number of lines that fit in your current terminal window. So if your terminal window is 80 rows tall a screen is probably 79 rows (one row is taken up for the status line), and a half screen is around 40\. But if you resize your terminal window the size of a “screen” changes accordingly. Still, take some time getting used to “scrolling” through the file quickly using the 1/2 and full screen motions, and getting a feel for how fast you can get around.

These motions are useful by themselves, and the better you get at them the more fun you’ll have in vim. But they get even better when combined with the *operators* and *counts* we’ll meet in the next two chapters.

## 6\. Operators 1: Changing Letters and Lines

Okay so, you’ve got line numbers, colors, and a basic idea of how to get your cursor from place to place. If you wanted, you could stop here, move the cursor around in normal mode, press `i` to go into insert mode, and make all your changes like you would in any other editor. But vim has a better idea. You can make a lot of the most common changes right from normal mode. For now we’re going to focus on the three most common commands: Cut, copy, and paste.

Only they have different names in vim. Remember that vi^([21](#chap35.xhtml_fn-veeeye)) has been around since before the whole “clipboard” metaphor was ubiquitous. So instead of “cut, copy, paste” it’s “delete, yank, put.” Let’s use a table to introduce the commands for some of the most common operators:

basic commands

| Keystroke | Command |
| --- | --- |
| d | delete |
| c | change (delete and enter insert mode) |
| y | yank (copy) |
| u | undo |
| p | put (paste) |
| r | replace (with whatever character you press next) |

To play with these three commands, let’s open up a sample document that we don’t mind really, *really* messing up. The sample documents folder has a file called `operators.txt` that would be perfect for this purpose.

### Operators Alone: Changing Single Characters

#### Killing Text

For the most part, operators by themselves work on a single character. The first section in `operators.txt` has words with duplicated letters like “ddoctor”, a not-uncommon mistake to make while typing. Getting rid of the extra letter is easy. Just position your cursor on the duplicated character and hit `d` (for delete) or `x` (for…a mnemonic that is supposed to simulate striking something out on a typewriter. I’m guessing the majority of people reading this book have never put in any serious time on a typewriter, so that little mnemonic is kind of obsolete now).

#### Resurrecting Text

Once you’ve deleted text it’s not actually gone, it’s in a *register*, or a special place in memory where vim can bring it back quickly if needed. In normal mode, pressing `p` will “put” whatever text was most recently yanked or deleted before the cursor.

#### Two Fun Ones

There are two operators that are useful in specific situations: `~` and `r`

`~` Changes the case of a single letter, while `r` lets you replace a single character with the next letter you type.

You can use both of these to correct line 13 of `operators.txt`, which reads:

```
1 "you can't grep a fred tree" --larry wall
```

Using the `~` operator three times ^([22](#chap35.xhtml_fn-threeTildes)) and the `r` operator once ^([23](#chap35.xhtml_fn-roperator)) you have a well formatted quote, even if the attribution may be a bit suspect.

### Operating on a Line

Changing single letters is fun and all, but sometimes you need to overhaul a line of text instead of a single letter ^([24](#chap35.xhtml_fn-words)). Vim includes shortcuts for changing a line into a more pleasing shape, like a shorter line, two of the same line, or no line at all.

Before we dive in, we should take a look at how vim defines what a “line” is and isn’t. Vim “lines” are everything between one press of the `<enter>` key and the next, even if that spans several visible “lines” on the screen. If word wrap is turned on vim will continue a line of text, like so:

```
1 8 This is the eighth line of text in this document.
2    It just rambles on and on. You'll notice that even though 
3    there are several sentences in this line, it still counts as a 
4    single "line" in vim, and there isn't a new line number until 
5    I press enter.
6 9 Okay, this is a new line, because I pressed enter. Which is why
7    there's a 9 over there in the line number column.
```

This is a useful way to think in programming, because you usually put a single statement on a line by itself. It’s less useful when you are working with long-form text ^([25](#chap35.xhtml_fn-longform)). When you’re writing prose in vim, it’s helpful to think “paragraph” instead of “line”.

#### The line must be drawn here! This far! No further!

Sometimes you need to cut the end off of a line, either to replace it with something else, or just to get rid of it. In vim, the uppercase versions of commands operate on the line from your cursor to the end of the line. Find the following line in `operators.txt`:

```
1 Emacs is a great operating system, it just needs a good editor.
```

You can make this sentence slightly less snide by positioning the cursor right before the comma, then pressing `D`:

```
1 Emacs is a great operating system
```

But then we’re left with a sentence fragment in search of a period. We can do better than that. Press `u` (for “undo) to restore the text you just deleted and let’s try again. If you press `C` vim will remove the same text as before, but this time it puts you in insert mode, ready for you to write something new here. All we want to do is add a period and then get back to normal mode, which seems a little wasteful. Press `<esc>` to get back into normal mode and let’s try one more thing. Press `u` to restore the text one last time. Okay, this time we’re going to combine two commands: Move your cursor one space right of the comma and press `D` to delete the text. Your cursor should now be *on* the comma, and you can just press `r.` to replace it with a period, all without leaving normal mode.

Put is a little different: lowercase `p` will put the most recently yanked or deleted text *after* the cursor, while uppercase `P` will put the text *before* the cursor. Here’s a demonstration: We’re going to say we cut the word `seven` from one line and want to paste it into the next line:

```
1 four score and |years ago...
```

In this situation, pressing `p` to paste would result in:

```
1 four score and yseven ears ago...
```

Because the cursor is “on” the letter y. But “yseven ears” isn’t what we want. but if you use `P` then you get the expected result:

```
1 four score and seven years ago...
```

The way you’ve always remembered it. And let’s be honest, that’s all of the speech you *can* remember.

#### A Whole New Line

To make the `d/y/c` operators affect an entire line simply duplicate the operator. So `yy` copies (or “yanks”) an entire line, `dd` deletes the line, and `cc` “changes” the line. (That is: deletes the line and puts you in insert mode). You can play with these as well in `operators.txt`, starting on line 31.

For starters, copy line 33, then paste it twice below to give three cheers for your vim knowledge. This can be accomplished by yanking the entire line, then putting it twice. This can be done in four simple keystrokes, once your cursor is on the line that says `- Hip Hip, Hooray!`. Simply hit `yy` to yank the entire line, then press `p` twice to paste it two times. Since copying an entire line also copies the invisible line break character, you don’t even need to move your cursor.

### Single Caps vs. Double Taps

Okay, we’ve introduced two ways to operate on a line instead of a single character. Let’s sum them up one more time.

To operate on an entire line you *double* the command, like `cc` to change an entire line, `dd` to delete an entire line, `yy` to yank an entire line, and so forth.

To operate on a line from your cursor to the end you *capitalize* the command instead. So `C` removes the line from your cursor onward and puts you in insert mode, `Y` yanks all the words from your cursor forward, and so forth. Here’s a quick example. Let’s say we want to get rid of half of the following line, because it’s backwards:

```
1 Four score and seven years ago years seven and score four
```

We would just put our cursor after the word “ago” and press `<shift>C` to get this:

```
1 Four score and seven years ago|
```

Type out the rest of the real sentence ^([26](#chap35.xhtml_fn-IfYouKnow)) and life gets better quickly.

Now a slightly more complex scenario:

Take the three somewhat muddled lines and put them in the right order. This can be done by deleting the line that is in the wrong place (which, again, removes the line-ending character, effectively moving the following line up a notch) with `dd` and putting it back where it fits with `p`.

### How to Instantly Make Your Life Easier with `cc` (or `C`)

There’s a common scenario in programming. You are declaring a new function and you want to make sure all your braces are matched from the get-go. So you set up your declaration, put an empty line in the middle, and set up your closing braces. Something like this:

```
1 $scope.awesome = function(arg){
2 
3 };
```

And then you move your cursor up to that middle line and… it’s right up against the left border, where you *don’t* want it:

```
1 $scope.awesome = function(arg){
2 |
3 };
```

You want your cursor to start properly indented, and you have probably developed a million ways to make that happen. When I was first starting my coding career I would position my cursor on that empty line, hit `<enter>` to create a new line, because that new line was usually properly indented by the IDE I was using, then go back and delete the improperly-indented line. And that trick will work in vim as well, but that’s no way to live.

Fortunately there’s a better way: just position your cursor on that empty line and hit `cc` (or `C` if you like that better). Think about what you just did: you told vim “delete everything on this line, and put me in edit mode.” Vim does that, takes a look at the lines above and below and does you one better: it puts you in insert mode with your cursor properly indented, all ready to write nicely formatted code:

```
1 $scope.awesome = function(arg){
2 	|
3 };
```

This is just another way that vim demonstrates its love for you. Note that this trick only works if you added the

```
1 Filetype indent plugin on
```

Like I suggested a few chapters back. I told you it would be good for something!

So, with all that under your belt go ahead and mess up the rest of the file moving and removing lines. When you’re feeling fairly comfortable with the process let’s move on to the fascinating topic of repetition. ^([27](#chap35.xhtml_fn-Repeating_myself))

## 7\. Doing Things More Than Once

One of the great things about vim is that it has been built for the way programmers work. We often want to jump to a specific word or symbol in the text without moving there line by line, or we want to replace the next four words with four new words, or other such silliness. It’s part of our job, and as I’ve said before, vim is all about making our jobs easier. It’s good at it!

Part of how it makes our job easier is by letting us *repeat* our actions as many times as we need to accomplish what we’re doing.

### Using Counts

This is usually accomplished by typing a number before you give vim a command. For example, let’s say you wanted to move the cursor four characters to the right. You could do this by typing `llll` or you could type `4l` and you just saved yourself *two whole keystrokes!* That’s money in the bank, friend. But as useful as it is to save two whole keystrokes, you can apply this concept to a lot of other motions and actions as well. Open up `counts.txt` in the sample documents and find this line

```
6 I am so incredibly stupid, useless, and talented.
```

Now, reading this, you realize that you need to get rid of the words `stupid, useless and`. You could delete those three words individually by putting your cursor before a word and typing `dw`^([28](#chap35.xhtml_fn-shortly)) three times, but why waste the time? Instead, put your cursor before the word “stupid” and type `3dw`. BAM! Just like that your sentence is much more indicative of you as a person:

```
6 I am so incredibly talented.
```

### Using Text Objects

Sometimes you don’t want to manually count how many characters you need to operate on. You want to delete the next word without counting how many letters are in it. Vim is here for you.

We’ve already covered part of this in a sneaky way in the “[Operating on an Entire Line](#chap07.xhtml_OoaL)”. If you double an operator you’re (usually) telling vim to apply it to the line as a whole. In this case, “the line as a whole” is what vim calls a *text object*.

If you’re a programmer you’re probably already familiar with the concept of objects: they’re the building blocks of most of the programming we’ve done since 1980\. But I’m going to go ahead and explain objects anyway.

In vim terms, a text object is a set of characters. It can be a single character, a few characters, a word, an entire line…all the way up to the entire document. Clever person that you are, you’ve already been using text objects in the last section. When you tell vim `d5l` what you are telling it is “the five characters to the right of the cursor make up a text object. Delete it.” If you told it `d5j` you’d be telling it that the next five *lines* constitute a text object whose presence is no longer required. But vim also gives us shortcuts for a number of other common text objects:

Text Object Shortcuts

| Shortcut | Text Object |
| --- | --- |
| w | from the cursor to the end of the word |
| W | from the cursor to the end of the WORD^([29](#chap35.xhtml_fn-wordvsWORD)) |
| s | the current sentence |
| ’ or “ | a string surrounded in quotes |
| l | from the cursor to the end of the line |

There are many *many* others, but this will get us going. When you combine an *operator* with a *count* and a *motion* you have a *command* ^([30](#chap35.xhtml_fn-count_terminology)).

For now let’s practice a bit. Open the file `counts.txt` and go to line 9\. There are four lines here that are just *begging* to be deleted. Let’s fulfill their wish, with three keystrokes. Using the **operator-count-motion** syntax you can just type `d4j` and those lines are *gone*.

Only they’re not. You can use counts with `p` as well. Go down a few lines and paste them back two or three times. We’re not sure when you’d want to paste multiple lines multiple times, but it’s worth playing with at the very least.

### Behold The All-Powerful Dot

This particular trick doesn’t have anything to do with counting, but it will be used with counted actions a *lot*. The `.` character, that simplest of all characters, is one of your best friends in vim. It’s meaning is simple: it repeats the last change you made to the text, but at your current position.

In `counts.txt` there’s a wonderfully contrived example: The simple “Jack and Jill” nursery rhyme, but somehow “Jill” got replaced with “Jack”. Which means the first line reads

```
1 Jack and Jack went up the hill to fetch a pail of water
```

That’s a good trick, Jack! Let’s fix up the second “Jack” using the change operator. Position your cursor after the letter J:

```
1 J|ack
```

And type `cw` (that’s “change everything from where the cursor is to the end of the word”). You should now have

```
1 J|
```

And be in insert mode. Type `ill` and hit `<esc>`. Now that the second Jack is a Jill, you can read through the rest of the poem and find any other mistakes. On the third line it says

```
1 And Jack came tumbling after.
```

Which makes no sense. Slap your cursor down like last time, but instead of typing `cw` you can just hit the period button and bam! Your last change is repeated with a single keystroke. If you’ve ever had to change all instances of a variable name in a file you can readily appreciate how useful this can be. It’s especially great when combined with [searches](#chap16.xhtml_searching), but more on that later.

The dot command is a good reason to be selective about what you do in insert mode, and how much you do between returns to normal mode.

## 8\. Moving Around in Vim: Dance Steps

Now let’s take everything we’ve learned about motion and give it a few last tweaks to make it really super useful. There are two text objects that look like they’re the same thing but aren’t. The difference between them can either cause you problems or make your life better. These text objects are *words* and *WORDS*.

### Words and WORDS

The easiest way to describe a WORD is that it’s every *character* between one whitespace and the next. Thus `http://I.am.a.frog.com` is a single WORD, even though you and I would parse it as six words^([31](#chap35.xhtml_fn-not-counting)). The lowercase “word” text object is any uninterrupted series of *letters*. Thus `http://I.am.a.frog.com` is made up of six “word” objects, separated by punctuation marks.

When you compose vim commands, you’ll specify that you want to operate on a “WORD” with a `W` and a “word” with a `w`, as you might expect. If you want to play with the differences you can check out `motion3.txt`, and have a look at the exercises there. Using the url above, you could position the cursor at the beginning of the word `frog` and change just that word with the `cw` command. If you wanted to change the entire string into something else you could put your cursor at the beginning of the line and type `cW` instead.

But always moving your cursor to the beginning of a text object to operate on it is a pain. Vim is smart, and can figure out where word boundaries are even if your cursor is in the middle of the word. You just need to tell it what boundaries you’re looking for. You can do that with the “inner” and “all” command modifiers.

### Inner and All

As you know, the text object commands `w s l` operate on the current text object (either a word, a sentence or a line, respectively. Check the [table](#chap31.xhtml_text-object-table) if you need a quick refresher) from your cursor position to the end. But what if you’ve got a long word like “Omphaloskepsis^([32](#chap35.xhtml_fn-omph-def))” and your cursor is somewhere around the first s? It’s silly to have to move your cursor back to the initial `O` just to be able to delete the word, and vim has a much better way.

You simply tell vim how to handle the *borders* of the text object in question and what to do with the text object. What constitutes a border depends on the kind of text object you’re using. A “WORD” is bordered by whitespace on both sides. A “word” is bordered by whatever isn’t a letter on either side. A sentence is bordered by a line ending or period. In general, vim works hard to match its concepts of borders to what humans think of as borders.

If you tell vim to operate on an *inner* text object it will leave the borders alone. For example, if I do a `diw` on the word “Galt” in the sentence `Who is John Galt?` we are left with `Who is John ?` Which isn’t grammatical, with that question mark floating around by itself at the end. However, if I were doing a `ciw` instead it would preserve the space between `John` and whatever new last name I want to give to Ayn Rand’s character:

```
1 Who is John Punchfist?
```

Much better.

However, when you’re straight up deleting text, you often want to modify *all* of a text object, spare whitespace included. To do this change the `i` in the previous commands to an `a`. If I had said `daw` on John’s last name in the example above the resulting sentence would have read `Who is John?` which is perfectly grammatical, if a bit vague, and nowhere near as awesome as asking who John Punchfist is.

You can no doubt see why I wouldn’t want to do `caw` there, because then I would have to *type* that space between “John” and “Punchfist” back in *all by myself*. Can you even *imagine*?

But `i` and `a` can do more than that. The “Inner” and “All” commands operate on just about any text object, including some fairly clever ones. Vim is smart enough to know that some symbols, like parentheses and quotation marks, wrap text objects that you may want to operate on as a whole. So it’ll let you! For example, consider the following sentence:

```
1 "Hello there! (He| lied)". Ted was always cheerful.
```

Not only is it terrible writing, it’s terrible grammar. But it’s a fun sentence to play with. Let’s say we want to get rid of the whole `(he lied)` bit. Easy! We’re going to tell vim to “Delete everything inside these parentheses, and take the parentheses with it.” It’s easier in vim speak, just type `da(`

Just like that you’ve got

```
1 "Hello there! |". Ted was always cheerful.
```

Now let’s say we want to change Ted’s greeting. Since your cursor is already inside the quotation marks you can change the text between quotes and leave the quotes alone. `ci"` is your command of choice, and you can make Ted say whatever you want:

```
1 "| ". Ted was always cheerful.
```

Vim is smart about these enclosures, and there are quite a few you can use. Here are a few of the more obvious ones:

Enclosures

| Enclosure | Meaning |
| --- | --- |
| `{` | Everything between two curly braces |
| `[` | Everything between two square brackets |
| `<` | Everything between two angle brackets |
| `t` | Everything inside the closest XML or HTML tags |

These all give you an easy way to modify exactly the text you want to change and nothing else.

### Move by Counting

We’ve already seen the beginning of this concept in the [Using Counts](#chap08.xhtml_counts) section, but let’s flesh it out a bit here. Motion commands are still commands, and you can tell vim to repeat them just like anything else. This means that you can move five words right by simply typing `5w`, or you can move six lines down: `6j`. This is often a faster way to get where you’re going than hitting `j j j j j j`.

But not always. The reason for this is the human ability called *[subitizing](https://en.wikipedia.org/wiki/Subitizing)*. Simply put, we as humans can easily recognize groups of things up to about three or four without counting them, but once you get above four we slow down considerably. In vim terms this means that if you look at a sentence and see that you have to move three words right you will just hit `3w` without thinking about it. But if you have to move six words right you’re probably counting those words, then entering the command, and that’s often slower than just mashing the `w` key six times, or (even better) just searching for the exact spot where you need to make your changes. More on that coming [soon](#chap16.xhtml_searching).

### (Book)marks

Every once in a while you want to get from place to place quickly and easily without counts, without searches, without doing anything but telling vim where you would like to go, thank you so very much. Kind of like a bookmark in your browser, but for a text file. That’s what *marks* are for.

A mark is just a pointer to a line in a file. If you set a mark at line seven of a file that’s where it will stay, giving you an easy way to return to line seven. But vim wouldn’t leave anything that boring or underdeveloped.

The marks are roughly divided into two groups: *lowercase* marks and *uppercase*, or*file*, marks. The obvious difference between the two is how you refer to the mark. The important difference is that lowercase marks are limited to lines inside a single file, while uppercase marks can jump freely to any line of *any* file. The two types of marks work in much the same way with slight differences. Let’s look at how to use lowercase marks first.

To set a mark you type `m` followed by a letter in normal mode. That’s all there is to it! Unless of course you want to get *back* to that mark later. Then there’s a little more. There are two ways to return to a mark. If you want to return to the exact character on the exact line where you set the mark you type a back tick (usually the same key as ~, right next to the number 1 on your keyboard) and the letter. So if you set mark `a` on line 5 you could then go anywhere else you want in the file and jump back to line 5 by typing

```
1 `a
```

If you only want to get to the *line* where you set the mark you can use a straight single quote (same key as double quotes, next to enter) and the letter. To get back to line 5 at the beginning you can just type

```
1 'a
```

And you’re good. But wait, there’s more! (There’s always more.) Whenever you jump to a mark, vim remembers where you jumped *from*, and stores it as a special mark `’` . So you can jump to line 5 with your `a` mark, make your change, and then just hit the single-quote key twice and you’re back where you started.

Naturally, you can do this with any letter from `a` to `z`, meaning you’ve got twenty-six marks you can set in any file you’re working on. But what about when you’re working on a bunch of files? That’s where the uppercase marks come in.

Uppercase marks behave the same way as lowercase marks, with one notable exception: they allow you to jump from one file to another with the greatest of ease. Like the lowercase marks, uppercase marks are set on a specific character of the file, meaning not only can you get from `sample.c` to `sample.h` in a single motion, you can get to line 471 of `sample.h` from anywhere with a single motion. But as much fun as it is to write c code, let’s talk about an uppercase mark that is instantly useful to every vim user everywhere. This is an exercise that you’ll definitely want to do.

*   Open your `.vimrc` file in vim.
*   Type `mV`
*   Open any other file in vim.
*   Type `'V`

Boom! You can now get to your `.vimrc` configuration file from anywhere at any time. While it’s true that you will eventually stop playing around with your configuration on a daily basis, when you’re first learning and configuring vim to work for you instead of against you this particular mark can save you a lot of time.

## 9\. Modes at Last

Given that modes are an integral part of vim, given that an understanding of modes is integral to using vim well, why did I decide to put off the chapter on vim’s modes until way into the text?

There are a couple of reasons. The first one is that I believe in learning by doing. By now switching between normal mode and insert mode should be fairly familiar, so the concept doesn’t seem so foreign. So now you’re ready to learn a bit more. So, without further ado, let’s get into vim’s modal nature. This is often the thing that scares people off, so we’re going to take it easy, and remember to breathe. Remember: you’ve already been using this stuff, we’re just putting names to things you’ve already been doing.

### What Modes Are

The simplest way to think about modes is that they change your keyboard. In *insert* mode the keys put letters on the screen, just like in a regular ol’ word processor. But when you switch into a different mode your keys change from letter-putters into command-makers ^([33](#chap35.xhtml_fn-letter-command)). The `h j k l` keys go from being four letters to being arrow keys, `.` changes from a full stop into the “do it again” button, and so forth. So far so good. You’ve been using both of these modes for a while now, and none of this is much of a surprise. What you don’t know is that you’ve been using a couple of other modes as well, and now that I’ve mentioned them I’m maddeningly going to go back to discussing normal mode and insert mode before I talk about two other modes that you never knew you were using.

### What is Normal, Anyway?

In *Mostly Harmless*, the fifth book in Douglas Adams’ *Hitchhiker’s Guide* Trilogy, there are animals called “Perfectly Normal Beasts” that suddenly appear out of nowhere on one side of a plain, thunder across the plain in giant herds, and suddenly disappear on the other side of the plain. Six months later they do the same thing, but backwards.

They’re called “Perfectly Normal Beasts” because someone was wise enough to realize that calling them that would help people accept their totally impossible behavior as something that just *happens*, not something to get all worked up about.

Normal mode in vim is almost entirely unlike that, but there’s a similar concept at work.

As you know, *normal* mode is where you issue commands, not where you edit text. Most newcomers to vim find this ironic in the extreme. After all, vim is a **text** editor, not a **command** editor. Shouldn’t editing text be the “normal” mode and “doing weird stuff with counts and operators and motions” be the “special” mode?

The answer, in vim’s mind, is “no”. And if you think about how you write software you’ll see why. In software development, you don’t just sit down, pound out code at 80 words per minute for 8 hours and then go home, a job well done. Software is written *incrementally* and *iteratively*, with a lot of time being spent looking at the interconnectedness of your various methods and variables and whatnot. You write a function header, give it some space between some curly braces for the function body, realize you forgot a needed parameter, add that, write some function code, realize you’ll need to call a new function you haven’t written yet, dummy that one up, and so forth. Coding isn’t as much like *writing* as it is like *drawing* ^([34](#chap35.xhtml_fn-write-draw)) .

When you draw, you start with some guide lines, an oval for a face, with crossed lines to give you dimensions. Rough outlines of background and scenery get sketched in, and little by little, line by line, the rough outlines are added unto, refined and turned into a finished product. It’s hard to say where they made the jump, but out of all those seemingly disconnected lines a work of art emerges.

Code is the same way. We add line upon line, sometimes putting in scaffolding code that will only be there for a little while, then be discarded when the logic it was supporting can stand on its own. It’s hard to say when, but somewhere in the process that seemingly random collection of lines of code ^([35](#chap35.xhtml_fn-seethere)) turns into a finished product. Well, okay, it usually happens when some manager says that we absolutely can’t miss another deadline or we’ll all be fired and we’ve got to ship something right now, but you get the picture.

Which is nice and all, but what does that have to do with “normal” mode not being “insert” mode? To answer that (here we go again) think of how an artist draws. They don’t sit there, staring at the paper with their pencil pressed against it. Nor do they drag their pencil across the page when they want to work on a different corner of the drawing.

And so it is with vim. Your “pencil” is your cursor, and for the most part it shouldn’t be sitting on the “paper” of your text file. You should be able to move it around without worrying about changing things along the way. This is the intent of “normal” mode. In normal mode you can move your cursor around and do quite a bit of very useful editing, but you won’t be adding new pencil strokes to the masterpiece that is your document.

### `--INSERT--` Means You Are Free to Type Normally.

Insert mode was also very carefully named. You can do a *lot* of editing from normal mode, but you can’t really add new text. To do that you need to have your keyboard turn back into a standard press-letter-keys-and-letters-appear keyboard, and that’s what insert mode is all about.

It still has a few tricks up its sleeve, though. We’ll get into some insert mode commands that let you make intelligent changes to the text without going back to normal mode. Since most of the heavy lifting is done in normal mode, insert mode is pretty light on commands, but there are a few. We’ll get into the fancier ones in the chapter on [Fancy Insert Mode Commands](#chap20.xhtml_ins-mode-commands) and a little bit in the chapter on [Registers](#chap14.xhtml_registers). For now we’ll just do two simple ones: `<ctrl>t` and `<ctrl>d`. These two commands are incredibly simple: `<ctrl>t` indents the current line by one tab (more or less) and `<ctrl>d` outdents it by the same with^([36](#chap35.xhtml_fn-indentoutdent)).

The application of this should be pretty obvious, especially if you work with structured code, like Python or HTML. lining up statements in a block makes them easier to read. But these two commands also show off an important point about insert mode commands: they all start with `<ctrl>` and a letter. See, this is the value of *Painless Vim.* Gems like that. In fact, I’m going to put it into a fancy tip block, just to reemphasize the point:

Okay, Let’s move on.

### Command Mode: The One You’ve Been Secretly Using all This Time.

So, technically, every time you press `:` in normal mode, you’re entering a brand new mode called *command mode*. You’ve been using command mode ever since page 1, where you typed `:q!` to get out of vim. And this demonstrates the majority of uses you’ll have for command mode. In general it’s used to issue commands to vim that have little or nothing to do with the text you’re editing. `:q` is a perfect example: quitting the editor is a *vim* command, not a *text* command.

We’re not going to deep-dive on command mode right now, just know that when you see a command with a `:` in front of it you’re probably looking at a system command.

### Visual Mode: Marking Text

Now we’re getting into new territory. Visual mode is one we haven’t hit on before at all. Visual mode is often fairly neglected, which is too bad because it’s also very useful. In Visual mode, you *visually* select an area of text to edit, instead of counting or searching or what have you. Basically visual mode lets you mark the beginning of a section of text, move the cursor to the end of the section, and then enter an operator to operate on that chunk of text. There are three ways to enter visual mode:

*   `v` enters “characterwise” visual mode. In this version you can edit an area as small as a single character, up to the entire document.
*   `V` enters “line-wise” visual mode. In this mode you can operate on one or more *lines* all at the same time.
*   `<ctrl>v` enters “block-wise” visual mode. In this mode you can edit a *block* of characters that can span rows and lines and can be pretty much any dimensions you choose.

All three types of visual mode have their uses, and we’ll go more into depth in the chapter on [Visual (Mode) Basics](#chap25.xhtml_visual-basics). But for now we’re just going to acknowledge that visual mode lets you select ranges of text visually and move on.

### …And all the Rest

There are other modes, of course. According to vim’s [built-in help](#chap17.xhtml_help) there are six “basic” modes and six “additional” modes, which are variants of the basic modes. But for the most part they’re not super useful, and *definitely* not painless, so we’re going to blithely ignore them, after pointing you to a reference^([37](#chap35.xhtml_fn-vim-help-modes)) where you can learn a whole lot more. [Here it is.](http://vimdoc.sourceforge.net/htmldoc/intro.html#vim-modes-intro)

## 10. Plugins

Vim is a great editor, but there is always room for expansion and improvement. Unfortunately, a small open source team can’t possibly keep up with every new language, technology, coding style, and theme needed to keep every developer in the world happy and productive. Fortunately, vim was designed so that those self-same developers can create *plugins* for vim that extend its functionality as new needs arise. Vim’s plugin system is as simple or as difficult as you want it to be. While the processes of creating a vim plugin is beyond the scope of this book, using them is something with which you should be intimately familiar.

### What a Plugin Is

In the simplest possible terms, a plugin is a set of new functions, shortcuts, and scripts that make vim work better in some specific way. It may be something as simple as syntax highlighting rules for the latest and greatest language to come down the pipe, or it could be an entire git repository management system. If you’ve ever added a new theme or extension to your browser you can think of vim plugins the same way.

There are a few ways to install plugins for vim, but we’re only going to cover two of them: the hard way (meaning the totally manual way) and the easy way. Since this book is called ***Painless** Vim* I would be remiss if I didn’t give you a nice link to the [easy way](#chap11.xhtml_easy-way) right here. So there it is.

### Plugins the Hard Way

Wow, you actually decided to read through this section. Okay! Well, that’s probably for the best, because even doing things the easy way you’ll have to go through these steps at least once.

Fortunately, the hard way isn’t really all that hard; it’s just very *manual*. It involves moving files around by hand and whatnot. Since I’m still shooting for a Painless type book I’m going to choose a simple plugin as our example. [Show Marks](http://www.vim.org/scripts/script.php?script_id=152) is a plugin that makes your marks visible, hence the name. To install it you have to do the following:

1.  Download the `.zip` file from the link above
2.  Unzip the file
3.  Copy the unzipped file into your `$HOME/.vim` folder
4.  Restart vim

Man! Dang, sorry about *all the hard work* there! Whew! I’m sweating from all that hard hard work!

Okay yeah it’s not that hard at all. But like I said, that’s an easy one. There are plugins that are significantly more complex, requiring you to copy *several* files into *several* locations…okay, it’s not ever all *that* difficult, but if you’ve got a lot of plugins it can get confusing to keep them all straight, and should you decide to get rid of one it can be a pain to clean up after that plugin and get rid of all the files it brought down with it. Fortunately, there is a (**much**) better way.

### And Now, the Easy Way

Unsurprisingly, there have been other people who have looked at the vim plugin installation procedure and decided that there is room for improvement there. While there are a number of plugins that help you manage other plugins, I’m just going to talk about one of them in depth. There are links to (and a few comments about) other plugin managers in the [appendix](#chap30.xhtml_plugin-managers). I’ll be covering [Pathogen](https://github.com/tpope/vim-pathogen) because it’s the one that I personally happen to like best.

Pathogen requires very little by way of setup, and the homepage has clear instructions on how to install it. The “copy and paste” instructions work exactly as they should. Once you’ve installed Pathogen, you can start installing other plugins simply by cloning them into your `~/.vim/bundle` directory and Pathogen will make sure they’re all loaded correctly when you start vim. That part is nice and easy to understand, but that’s only half of the value. Pathogen is set up to put each plugin in it’s own directory, meaning it’s trivial to remove a plugin should you decide you don’t like it any more. You just delete the plugin’s folder from the bundle directory and restart vim.

Once you have installed some favorite plugins just restart vim and they should be ready to go. But wait, there’s more! (there’s always more). Pathogen gives you a single command to integrate the help files from each of the plugins you’ve installed into Vim’s [help](#chap17.xhtml_help) system. All you have to do is run `:Helptags` from the vim command line and it will scan all the plugins and get the help system set up. One step, no problems. You could put the `Helptags` command in your `.vimrc` file, but the author of the plugin doesn’t recommend it.

#### Let’s Install a Plugin!

Okay, let’s put the rubber to the road. I’m going to operate under the assumption that you have already installed Pathogen following the instructions on the Github site. Once that’s done we can move on. Go ahead. I’ll wait.

Okay! Let’s install the [Commentary](https://github.com/tpope/vim-commentary) plugin. This plugin makes it trivial to do line and block comments in many types of files using some pre-set keystrokes, and is super-useful for all of us programmer types. So, all that said, follow the steps below to install Commentary:

*   Open a command line
*   Enter the following at the command line:

    cd ~/.vim/bundle

    git clone https://github.com/tpope/vim-commentary.git

*   Start up vim and type `Helptags`

Okay! The plugin is all kinds of installed now! To learn more about how Commentary works just type `:h commentary` and vim will start up its help viewer to show you everything you need to know. If you’re still afraid of the help system, that’s understandable. You can wait until the chapter on [Help Files](#chap17.xhtml_help). It’s coming right up.

### Nate’s Favorite Plugins

Remember that whole “opinionated” thing from the introduction? Well, here comes a whole wave o’ opinions. These are plugins that I like and use on a daily basis. Feel free to check them out and see if they work for you.

#### CtrlP

[CtrlP](https://github.com/kien/ctrlp.vim) gives you fuzzy matching file finding, a la SublimeText or Textmate. If you don’t know what that means, you just hit `<ctrl>p` and start typing any part of the path or filename you can remember and the plugin will find the file you mean. It’s wonderful.

#### NERDTree

![The NERDTree in action](images/NERDTree.jpg)

The NERDTree in action

[NERDTree](https://github.com/scrooloose/nerdtree) provides a nice sidebar to vim that gives you a file explorer, much like you’d see in any other text editor. This makes it easy to find the file you want to work on. If you decide to use NERDTree I would recommend adding a line to your `.vimrc` like the following:

```
1 noremap <Leader>n :NERDTreeToggle<CR>
```

Don’t worry about what all is going on there (we’ll cover it more in the chapter about [Key Maps](#chap19.xhtml_mapping-keys), but the upshot is that you can type `\n` and have the NERDTree sidebar pop up. Then you can choose a file to edit and dismiss the sidebar with the same `\n` keystroke. When you get a little more comfortable with vim you can also use single key commands in NERDTree to edit files in their own [window](#chap21.xhtml_windows) or [tab](#chap22.xhtml_tab-pages).

#### Fugitive

If you use git in any of your projects [Fugitive](https://github.com/tpope/vim-fugitive) is one of the best things to happen to vim. It gives you a simple and clear way to perform all the git commands you need without leaving vim. You can stage or unstage files simply and quickly, commit them from the same window, then go back to editing your source code. (More on (windows soon)[#windows].) One of the nice things about Fugitive is that it comes with a lot of keyboard shortcuts built in to make doing all the things you would normally do even easier; things like staging a file (position your cursor on the line and press `-`) and committing the staged files (type `cc` in the Fugitive window). Suddenly git and vim are best friends.

#### Zen Coding

[Zen Coding](https://github.com/mattn/zencoding-vim) provides support for the fabulous [Emmet Toolkit](http://emmet.io/). If you haven’t played with Emmet yet, it’s a way to quickly write something like:

```
1 html>head>title{This is a webpage!}^body>p{Some text!}
```

and simply press `Ctrl+y` to have it expand into

```
1 <html>
2    <head>
3      <title>This is a webpage</title>
4    </head>
5    <body>
6      <p>Some Text!</p>
7    </body>
8  </html>
```

In essence, you just write what you mean and emmet turns it into HTML. It’s pretty great.

#### Vim Colorschemes

I only kinda recommend this one. [Vim Colorschemes](https://github.com/flazz/vim-colorschemes) packs a few hundred of the most popular colorschemes into a single plugin. Once installed you can switch to any of them by just changing the `colorscheme` line to whatever scheme you want to use. Most of them are pretty solid, battle tested schemes that a lot of people have used, but this is definitely a case where your milage may vary.

The reason I “only kinda” recommend this one is that it’s entirely possible to waste a whole day choosing your favorite colors for things. Not that I would ever do that. Five times a year. I mean, it’s not like I’ve already switched color schemes once in the middle of writing this book, or anything.

Seriously, choose one you like and then stick with it forever or else you’ll go insane. Save yourself!

## 11. Operators: Moving and Changing at the Same Time

So, now that you know all about counting and Operators and all the nuances of moving the cursor around, we’re going to solidify our understanding of how motions and operators can work together.

### Move-and-Edit Commands; or “Vim Commands 202”

Okay, we’re going to re-hash a little here. A vim *command* consists of:

*   An *operator*
*   A *count*
*   A *motion*

Depending on the situation, all three are optional. If you type `4` by itself vim will wait for you to tell it what to do four times. So you can give it a motion, like `j`, and it will move the cursor down four lines. Or you can give it an operator like `p` to paste something four times. Or you can give it both an operator and a motion, like `dl` to delete the next four characters.

The last one is an example of *editing by motion*. Deleting a bunch of lines at once is just the tip of the iceberg. The great thing about learning to edit in this way is that once you’ve got the hang of it you can combine commands to make any change you want. Let’s take a look at something I’m doing at work right now: Writing a `Gruntfile.js` configuration script for the [Grunt](http://gruntjs.com) automation system.

What Grunt does is immaterial to the discussion; for now all we need to know is that there’s a section that looks like this:

```
1   grunt.loadNpmTasks('grunt-contrib-jade');
2   grunt.loadNpmTasks('grunt-contrib-watch');
3   grunt.loadNpmTasks('grunt-contrib-sass');
4   grunt.loadNpmTasks('grunt-contrib-concat');
5   grunt.loadNpmTasks('grunt-contrib-less');
6   grunt.loadNpmTasks('grunt-contrib-uglify');
7   grunt.loadNpmTasks('grunt-contrib-clean');
8   grunt.loadNpmTasks('grunt-contrib-copy');
```

And so on for a bunch of lines. Now, I could have entered each of these lines by hand, but that’s just stupid and painful and pointless. Vim made it much faster. The nice thing is that there are a couple of fast ways to do this, depending on how much thinking ahead you were able to do. Let’s look at some repetitive editing tasks, from the least forethought to the most.

#### Least Forethought: Copy this line

So, let’s say I typed the first line, and realized that I’m going to add another line just like it. I start out with this:

```
1 grunt.loadNpmTasks('grunt-contrib-jade');
```

And with my cursor at any point on that line I type `yyp`. In other words “yank the entire line and paste it.” Now I have

```
1 grunt.loadNpmTasks('grunt-contrib-jade');
2 grunt.loadNpmTasks('grunt-contrib-jade');
```

Which is close to what I want. I can get my cursor to the word `jade` in the second line, type `ciw` and replace it with the word `watch`. There! I’ve added a new line. What’s more, I can just type `p` and I’ll have a third line that I can modify in the same way. I can keep doing this until I’ve got all the modules I need listed in my `Gruntfile`.

#### Slightly More Forethought: Copy this line. **A LOT**.

Okay, so let’s go back to square one: I’ve got the first line written, and I realize that I’m going to need more than one copy of the line. No problem. But since I’m thinking ahead this time I’m not going to copy the word `jade` because I’m just going to change it in all of the copies. So I’ll delete the word right now, giving me

```
1 grunt.loadNpmTasks('grunt-contrib-');
```

This has the added side-benefit of throwing an error if I try to run grunt, since that’s not a real module. A little added error checking is a good thing, I say.

I’m thinking ahead, so instead of just hitting `p` to give myself a new copy I hit `7p` and have seven new lines ready for me to edit. Not bad! Now, I realize that sometimes you don’t *know* how many nearly-identical lines you’ll need, but we’ll pretend it’s more common than it is, because otherwise the next section is *entirely* pointless.

#### Uncanny Levels of Forethought: Knowing how many copies you want *Before you start typing*

Let’s say that you know, right this moment, that you’ll need 8 copies of a line that you haven’t even typed. Good for you! You can do this all in one step, and here’s how. Ready? Watch close, this’ll go by fast:

```
1 8i grunt.loadNpmTasks('grunt-contrib-');<enter><esc>
```

And you’re there. You can see that all we did was put a count (namely, *8*) before the “enter insert mode” operator `i`. So we told Vim to re-do anything we do in insert mode eight times. This is awesome, no?

Again, I realize that it’s not always what you want to do, nor is it even OFTEN something you want. But knowing about it is useful for two reasons: one, you can pull this trick when you need it, and two, you can figure out what just happened when you pull a trick like missing the `G` key and instead of *going* to line 55 and typing something you type something right where you are, then copy it 55 times. Not that I’ve ever done that. Today. In this chapter.

*Cough*

What?

#### The Triumphant Return Of The Almighty Dot

Okay, but here’s the most useful edit-by-motion command you’ll ever see *ever*. Let’s say you’ve got a file where the indentation is all messed up, and there are entire methods that are over-indented. In the old days (assuming you weren’t using Sublime Text in the old days) fixing this involved using the *mouse* to *highlight* all those lines and then hit `shft-tab` to un-indent that method. Vim can do you one step better. If you can quickly count all the lines you want to operate on at once, you can just put that number in front of the `<<` command and all your lines are moved back one tab, all together.

“But Nate,” you’re saying, “The dot command wasn’t in there *at all*”. You’re right, grasshopper. I was just easing you in. What’s the other most common thing you have to do to a whole freaking boatload of lines all at once? That’s right, it’s *indenting* them. ^([38](#chap35.xhtml_fn-Kidding)) Let’s say you make the edit to a single line and realize that you’re going to have to do this over and *over*. Don’t. Move your cursor to the first line in the set that still needs edited and type `8.`

In other words “make that last change on the next 8 lines.” Suddenly anything you can do once you can do over and over again, without even thinking about it all that hard. It’s kinda fun.

It’s also a good reminder about our advice earlier about making *small* changes. The smaller a change is the easier it is to repeat and the more likely it is to be worth repeating.

## 12\. Interlude: How to Back Off Without Giving Up

Let’s face it, there are going to be times where you are sick to the *eye teeth* of vim and all its stupid weird commands and modes and just want to do some actual *work*. I get that. Even now I do that from time to time. Sometimes it’s nice to feel like you’re back in control instead of the student of some crazy workaholic teacher.

There are two ways to make yourself feel better in moments like this. The first is to just go ahead and fire up your favorite editor and get to work. Use the arrow keys, all those other shortcut keys that are integrated into your OS, and just live the good life of a person who has a tool they like.

Just don’t blame me if moving around using the arrow keys suddenly feels *intensely* awkward, or if you keep typing `jjkj` in your text trying to move up and down. It happens. It can be a little disappointing, but it’s part of growing up. In a way it feels kind of nice. You’re getting good at vim and starting to see the power there, and starting to realize how limiting other editors can be.

The second way to help yourself feel better is to see if your favorite editor has a “vim compatible” or “vim emulation” mode. Many of them do. Once you enable this mode you can use as much or as little of the vim stuff as you want while still being well and truly productive in an editor you’ve already learned how to use. This way you’re not really giving up on learning vim, you’re just using what you’ve learned to make you more productive in, say, IntelliJ or Sublime Text.

Sublime Text, by the way, does a good job of implementing pretty much all of vim’s commands ^([39](#chap35.xhtml_fn-noO)), and as an added bonus to people who are tired of starting up in “normal” mode, it always starts you into insert mode. So, you still have access to all the quick motion features of vim, all the shortcuts and easy editing methods, with all the added bonuses of a modern editor and even–glory be– *mouse support*.

Coincidentally, if you decide that vim isn’t your cup of tea, you could do far worse than using [Sublime Text](http://www.sublimetext.com/) as your new editor of choice. Its built-in ^([40](#chap35.xhtml_fn-disabled)) “Vintage Mode” does a great impression of vim, and it takes a lot of vim-like ideals (quick motion, mouse-free *everything*, text-only configuration, nearly infinite extensibility and configuration) into the modern era, and adds on a metric ton of good ideas all its own. In fact, my quest to learn vim started as a desire to use Sublime Text more efficiently.

And no, nobody is paying me to say any of this.

## 13. Registers: Clipboards as Far as the Eye Can See

Whenever you yank or delete text it doesn’t just disappear into the universe. Just like modern operating systems, vim keeps that text around in an area that your OS probably calls a *clipboard*, but vim calls a *register*. Unlike most operating systems, however, vim gives you a **lot** of registers to play with, instead of just one. When you just type `dd` or `yy` vim copies your text into its default register, which is paradoxically named “the unnamed register”. Likewise, when you hit `p` vim just pastes the text from this unnamed register without asking any stupid questions.

### Say Hi to the Named Registers

However, you can use a lot of other registers as well, and access those registers using all the operators you already know and love. For example, if we cut the word “cat” from the following absolutely fascinating sentence:

```
1 I have a cat bed.
```

We want to make sure that our cat doesn’t get clobbered the next time we cut or copy something, so we’ll store it to a *named register*. Every register in vim is prefixed by a double quote: `"`. And the named registers are each named after a lower-case letter of the English alphabet. So you’ve got `"a`, `"b`, `"c` and so forth, which we read as `register a`, `register b`, `register c` and so on. Since we’re storing a cat, let’s put it `register c`. We do that by telling vim which register to use and what to do. So put your cursor before the letter c in cat and type:

```
1 "cdw
```

Which, in vim speak, means “You know register c? Okay, good. Cut this word and put it there.” And just like that, your text is stored in `"c`, which we pronounce `register c`. Now if we want to paste the cat back into our text somewhere else we just type

```
1 "cp
```

And you’re golden.

But what about the unnamed register? You know, the one that *everything* gets cut or yanked into? What if we want to paste something from that register?

Well, we’d just press `p` like we always do. But if you wanted to *explicitly* paste whatever is in the unnamed register, you can contact the unnamed register directly using two double quotes in a row, like this ^([41](#chap35.xhtml_fn-regnames)) :

```
1 ""p
```

### Little Changes, Big Changes

When you yank or cut text, it gets stored in two places. The first is the unnamed register ^([42](#chap35.xhtml_fn-ThreeReg)) The second, however, depends on what change you made to the text. If you just *yanked* some text using `y` then a second copy is stored in the yank register, which we call `0`. If you cut a few words but not a whole line your second copy is in the “small delete” register: `-`. But it gets more interesting when you cut one or more lines.

Remember that vim is a programmer’s text editor, and as such is aware that lines of code are important. So every time you cut an one or more lines the text you just cut gets stored to register **1**. If you cut another entire line the it doesn’t overwrite what was stored in **1**, it just bumps it to **2**, and the text that was stored in register **2** moves to register **3**, and so on to register **9**. In this way you can be carting around nine major code snippets as you edit your text. Even better, these registers aren’t erased when you close vim ^([43](#chap35.xhtml_fn-Viminfo)) .

To get a better handle on this, let’s play with cutting lines and moving them around in the file `registers.txt` from the sample documents repo. Near the beginning of the file there are four lines that are out of order like so:

```
1 - Four
2 - Two
3 - Three 
4 - One
```

We can put them back in order pretty easily by just deleting each line using `dd`. This pushes them onto the large delete register stack. But what if you can’t remember what order they were stored in? Vim has you covered. If you enter `:reg` in normal mode you’ll get a screen popup that lists all the current registers and what they’re storing. You can even enter a command (like, say `"1p`) from this screen. Otherwise you can just look at the order your lines are in and paste them back into the text in the right order.

### Really Actually Deleting Stuff

But what if you want to get rid of something without clobbering the unnamed register or adding it to the large delete stack? There’s a special register, affectionately called “the black hole register” that can be used for just that purpose. You can’t pull text *from* this register any more than you can pull matter out of a real black hole. It’s useful when you just want something gone, and you access it using `_`. So if you have a line of text like this:

```
1 I hate everything!
```

And you want it gone for good, just put your cursor anywhere on that line and enter

```
1 "_dd
```

to send it spiraling out of existence^([44](#chap35.xhtml_fn-notforever)) without touching anything in any of your registers.

That was a lot to take in all at once, so let’s sum it all up in a fancy table:

Named Registers

| Register Keystroke | Name | What Goes In It |
| --- | --- | --- |
| `""` | The Unnamed Register | Every cut or copy |
| `"_` | The Black Hole Register | Anything you want to get rid of |
| `"\` | The Last Pattern Register | A copy of the last thing you searched for |
| `"-` | The Small Delete Register | The last cut or copy that was less than one entire line long |
| `"1` | The Big Delete Register | The last thing you cut or copied that was 1 or more lines long |
| `"2-"9` | Big Delete Register Stack | A running stack of big deletes. `"1` gets pushed to `"2` and so on |
| `"+` | The System Clipboard | If it works. It doesn’t always work |
| `"a-"z` | The Named Registers | Anything you want |
| `"A-"Z` | The Append Registers | Using `"A` will *append* to register `"a` instead of *overwriting* it |

## 14. Text Origami. `:h folding`

This isn’t a complex topic, nor a particularly huge one. But it’s worth knowing how to handle text folding in vim, because it’s just a little more involved than you’re probably used to.

If you’re not familiar with the concept, *text folding* means taking parts of your document and hiding them, as if you’d folded the document so that the text above the fold and the text below the fold are right next to each other. When you fold text in vim it definitely lets you know that something is up:

```
1   function Sample(data){
2   +--- 5 lines: //TODO: write a real method here----------------------
3 
4   };
```

Depending on your chosen theme^([45](#chap35.xhtml_fn-current-theme)) the fold markers may even be highlighted to make them even more noticeable. But before you can go around folding up text you need to tell vim *how* you want it to fold things. You’ve got a few options, But if you’ve been using folding in other editors you’re probably going to be comfortable with either `syntax` or `indent`. Let’s look at how to set this up:

If you just want to play with folding for a while you can run `:set foldmethod=indent` from the command line. This will give you a simple folding scheme to play with, and decide if you want to keep it. If you like it you can always make it permanent in your `.vimrc` file later. The `indent` folding method just looks at the whitespace at the beginning of a line and folds everything indented that much or more. So if you have a passage like this:

```
1 <html>
2   <head>
3     <title>Old School Simple HTML!</title>
4   </head>
5   <body>
6     <p> I am a simple paragraph!</p>
7   </body>
8 </html>
```

Then you can position your cursor at the beginning of the `<head>` tag and trigger the fold mechanism. Do that and you’ll have this:

```
1   <html>
2   +--- 6 lines: <head>-----------------------------------------
3   </html>
```

This may not be exactly what you’re expecting, but it’s what you told vim to do. Everything at the same indentation level as the line is folded away nicely. If you just wanted to hide stuff in the `<head>...</head>` section you can either move your cursor to the next line down and fold from there, or you can try to use *syntax* folding.

Run `:set foldmethod=syntax` to make the switch. While syntax folding is more or less what you would expect, there are some new caveats involved in it’s use.

The first is that foldable areas in a language are defined by the same module that vim uses to determine syntax coloring. If that module doesn’t have information on what constitutes a foldable area you won’t be able to use syntax folding. This isn’t a problem in languages like, C/C++, Java, ruby, python, etc. which all have large, active communities that have ensured the language modules are complete. But if you’re using a more uncommon or unsupported language the support is somewhat hit and miss. Still, it’s a little closer to what you were probably expecting.

### Okay, But How Do I *Fold Things*?

It’s a fair question. Let’s go back to indent-style folding quick and work through some basic scenarios from there. In this mode you can position your cursor at the beginning of a line and fold all the lines in that region with `zc`^([46](#chap35.xhtml_fn-cIsClose)). To reopen a folded region you type `zo`(The “o” is “open”). The cool kids use `za` to toggle a section between its open and closed states, but it’s worth knowing all three commands, just in case.

But wait, there’s more! (There’s always more). Using commands that operate on a single fold is such a drag, no? If you want to operate on entire passages all at once there are a set of commands that do that too. Let’s say you’ve got some python-esque code like the following:

```
1 friends = ['Monique', 'Rachelle', 'Toby', 'Russ', 'Francis', 'Regina']
2 for name in friends:
3 	 if name != 'bob':
4   		print "Hello {name}!".format(name=name)
```

Okay, I’m not a python genius. But that’s not the point. The point is that you can fold the entire `for` loop as well as the sub-folds within using the `zC` command. Yep, using a capital letter makes the folding commands work recursively instead of individually. `zO` and `zA` work as you would expect them to.

But let’s say you don’t *care* where your cursor is and you just want to see a lot more of your file than you can at present. That’s where `zr` comes in. When you type `zr` you *reduce* folding by one level document-wide. So if you have a fold inside a fold you will now only have one fold. If you want everything in the whole buffer unfolded you can power up your *reduce* command by shifting to uppercase: `zR`.

The opposite is `zm` and `zM`. Lowercase folds up the innermost folds all across the document, uppercase folds up *everything*.

Okay, that was a lot of commands interspersed with a lot of words, so we’re going to go for the big bad table o’ commands now for easy reference. (This table is also included in the [Appendix](#chap31.xhtml_Appendix-2))

Folding Commands

| Command | Option |
| --- | --- |
| `zc` | Close current fold |
| `zo` | Open current fold |
| `za` | Toggle current fold |
| `zC` | Close all possible folds at cursor |
| `zO` | Open all possible folds at cursor |
| `zA` | Toggle all possible folds at cursor |
| `zr` | Reduce folding by one level throughout the document |
| `zm` | Increase folding by one level throughout the document |
| `zR` | Open all folds |
| `zM` | Fold everything |

## 15. Searching and (More Importantly) Finding

Vim wouldn’t be what it is without a good search function built in to the editor. Vim’s search functionality is super powerful and surprisingly intuitive…once you get used to it.

Before we get started, I want to point out that vim searches come in two flavors: **forward** and **backward**. For each *type* of search, you can do that search from your cursor to the *end* of the document (which is the **forward** style) or from your cursor to the *beginning* of the file (which is the **backward** style). In most cases, searches will wrap when they hit the end (or beginning) of the document. I’ll list the search commands with the **forward** style first and then the **backward** style.

### Whole File Searches: `/` and `?`

One of the most common types of searches you’ll do is searching the entire document for a word or term. To start this kind of search hit `/` or `?` and your cursor will jump down to the command line on the bottom of the screen. Type what you’re searching for and press `<enter>`. Vim will highlight all the occurrences of the word you typed, and position the cursor at the occurrence of the word closest to your cursor. You can then jump to the next match using the `n` button. Remember that if you started the search using `?` the “next” match will be the match closer to the *beginning* of the document, not the *end*.

But what if you want to *reverse* the direction of your search? Let’s say you hit `?` when you started your search, but you want to start moving toward the *end* of the file now? No problem. Pressing `N` (that’s an uppercase N instead of a lowercase n) will jump to the *previous* match, meaning the closest match *against* your direction of search.

Confused yet? I strongly encourage you play with these searches for a few moments in the `searching.txt` file, looking for the [Illuminati’s secret mind control word](https://en.wikipedia.org/wiki/Fnord#Definition_and_usage).

### Find Me Another One of These: `*` and `#`

Sometimes you want to find the next instance of the word you’re on. This is especially useful in programming, where you might be trying to find all the places where a certain function is called or some such tomfoolery. In `searching.txt` you might want to find another copy of a word like “fnord”. In Vim this is simple: position your cursor on the word you want to find and press `*` or `#`. You can jump between matches using `n` and `N`, just like with the whole file searches.

### Line Searching: `t/T` and `f/F`

There are times where you just want to jump a few words forward or back along a line without hitting `w` or `b` over and over again. Once again, vim is ready, this time with not one but *two* types of searches.

If you type `t`*x* (or `T`*x*, for a reverse search) your cursor will jump “to” the closest occurrence of *x* in the line you’re on. However, this might not work the way you were expecting. This “to” search will drop your cursor one character *before* the letter you searched for, like so:

```
1  | I'll Be There For You/When the Rain Starts To Fall 
2 -> tF 
3  I'll Be There| For You/When the Rain Starts To Fall
```

I don’t know *why* vim does this, it just does. It’s worth noting that when you do a reverse search using `T` your cursor will be positioned one character *ahead* of the letter you typed. Again, I don’t know why. But at least it’s consistent.

Fortunately, you’ve also got the `f`*x* search method, which works the way you would expect:

```
1 | I'll Be There For You/When the Rain Starts To Fall   
2 ->fF 
3 I'll Be There |For You/When the Rain Starts To Fall
```

In both cases, you use `;` to jump to the next match and `,` to jump to the previous match, unless you’ve [remapped the comma key](#chap19.xhtml_what-map), but we won’t get to that for a couple more chapters yet.

### R…R…Regular Expressions?!?

If you are already a fan of regular expressions for text manipulation then this is a good section for you. If you’re not sure what a `/reg(ular)\s?ex(p|pression)/` is than I would point you to some [excellent](http://www.amazon.com/gp/product/0596528124/ref=as_li_ss_tl?ie=UTF8&camp=1789&creative=390957&creativeASIN=0596528124&linkCode=as2&tag=httpnatedicco-20) [resources](http://www.regular-expressions.info/) on the topic, and probably suggest that you skip the rest of this chapter. It’s not that I don’t want you here! It’s just that *learning* regular expressions isn’t exactly *painless*. It’s *valuable*, but it takes time and effort.

Vim does let you search and replace using regular expressions, or “regexes” as they’re called by people who can never figure out how to pronounce “regexp”. So, that’s the good news. The bad news is that vim uses a regular expression engine unlike any you’ve ever seen.

It starts out normal enough. If you want to search and replace a word you simply type `:s` followed by the usual regular expression replacement syntax:

```
1 :s/old/new
```

And the next instance of the world `old` will be replaced with the word `new`. Simple, right? Okay. Let’s go one step further. Now you don’t want the word `old` anywhere on the current line. In this case just put the letter `g` at the end of the string, which makes it a “global” search, although in this case a “globe” means “one line of text.” Don’t ask me. The point is you can remove all occurrences of the word “old” from a single line using this command:

```
1 :s/old/new/g
```

So far, no big deal, right? Okay. Let’s say that you don’t want the word `old` anywhere in your document at all. Okay, no problem. We’ll tell vim to search the *entire* document and sub in `new` for `old`:

```
1 :%s/old/new/g
```

What is that percent sign doing there, you ask? Remember clear back in the beginning of the book where we re-loaded our `.vimrc` file using the command `:so %`? Then, as now, the percent sign means “this here current file”. So in this case we’re telling vim to replace every instance of `old` in this here current file.

Okay, now let’s get tactical about it. Let’s say that the word “old” is only *persona non grata* between lines 25 and 50 of the document. You can tell vim what range you want to search using the following `start,end` syntax:

```
1 :s 25,50 /old/new/g
```

“Wait,” you say. “I’m scared! I’m afraid that the changes I made are wrong and will ruin the world!” Vim understands. Sometimes you don’t want vim to change every instance of the word `old` without getting your stamp of approval first. You can do that. All you have to do is add the letter `c` (for “confirm”) to the end of the command, like so:

```
1 :%s/old/new/gc
```

When you hit `Enter` Vim will jump to each instance of “old” and ask if you want to change it. If you press `n` it will leave the word alone. If you *confirm* the change by pressing `y` it will make the change. Handy, no?

##### Where it Gets Ugly

“This,” you are no doubt saying to yourself^([48](#chap35.xhtml_fn-good_at_regex)), is no big deal. This is just regular old *regular expressions*, not something to be worrying about. Well, I was just easing you in. Here’s where it gets ugly.

If you are a fan of the expressions most regular, you don’t waste too much time before you start putting parts of your search in groups and using those search groups to make your life better. Let’s say you want to do something simple like find a string of six hexadecimal characters. In most modern regular expression parsers^([49](#chap35.xhtml_fn-pcre-parsers)) you would type something like:

[0-9a-f]{6}

In other words “Match any character between 0 and 9, or a-f six times”. This is basic stuff.

And here’s what vim does odd. Instead of letting you just wrap a section in parentheses, you have to *escape* the parentheses, or else vim will search for them. **I know.** So if you wanted to run the search above using vim, you would write it thus:

\[0-9a-f\]\{6\}

And that’s a *fairly simple* regular expression. When you start having nested brackets and “or” clauses (which use the pipe symbol `|` ) you can reach a point where it feels like half of your regex is backslashes.

#### You Have to Believe Vim is Magic!

Fortunately, there’s hope. Vim hasn’t been static in all the years since vi, and while the old vi regex syntax is still the norm, you can override it without too much work. Vim has two special search modes called `magic` and `very magic`. Magic searches behave a lot more like POSIX style regular expressions, while **Very Magic** searches are more or less what you’re used to if you learned regular expressions using Perl, Ruby, Python etc.

To access the “magic” or “very magic” search modes, you just prefix your search with `\m` (for magic) and `\v` (for *very* magic) mode. As you might expect, both magic and very magic modes have their opposites, which are triggered by using an uppercase `M` and `V` respectively. It’s worth knowing exactly what you’re getting into with each search mode, which means it’s just about time to break out a fancy ol’ table.

Vim Regex Modes

| Mode | `\v` | `\m` | `\M` | `\V` |
| --- | --- | --- | --- | --- |
| Name | Very Magic | Magic | *Not* Magic | *Very* Not Magic |
| End of line | `$` | `$` | `$` | `\$` |
| Parentheses | `( )` | `\( \)` | `\( \)` | `\( \)` |
| Alternates | `&#124;` | `\&#124;` | `\&#124;` | `\&#124;` |
| Repeats | `*` | `*` | `\*` | `\*` |
| Any Character | `.` | `.` | `\.` | `\.` |
| Literal dot | `\.` | `\.` | `.` | `.` |

As you can see, magic mode is an odd mix of not-magic and very magic, which makes it kind of an annoying set of rules to remember. Before we get into any suggestions, here’s a basic rundown of how each mode works, in descending order of magicality:

*   **Very Magic**: In this mode *every character* other than letters, numbers and underscores are *special characters*, meaning they modify the search instead of being a search term.
*   **Magic**: In this mode *some characters* are special characters and others aren’t. While this is vim’s default search mode, it’s also the least consistent.
*   **Not Magic**: In this mode *few characters* are special characters. In general you will have to escape things like parentheses or brackets to give them special character powers.
*   **Very Not Magic**: In this mode *only the backslash* is a special character. All characters in the search string will be interpreted literally unless preceded by a backslash.

There’s quite a bit more to know about vim’s built-in regular expression engine, but at this point I’m going to point you at vim’s built-in help to learn about it. If you type `:h search-pattern` in normal mode you’ll be ready to embark upon a whole world of reading about how searches are conducted in vim.

And if you’re still afraid of vim’s built-in help system, well, that’s what the next chapter of *this* book is all about!

## 16\. Using Vim’s Help System

So, clear back in the introduction I spoke about how the help system is a pain to use. And for a newcomer it kinda is. But like everything in vim it’s only irritating while you’re learning to use it. Once you’ve mastered it you’ll find the help system incredibly useful and almost *intuitive* even.

Okay, the basics: When you type `:help` in normal mode you’ll suddenly have your vim screen split in half, the top half showing you a help file, the bottom half showing whatever you were already working on. Your cursor is up in the help window, and all your motion commands work like they always have: you can go up and down by half or whole pages, jump to the top or the bottom, the works. Which is nice and all, but the first question that most people have with when faced with this screen is “how do I make it go away?” That’s a good question. Without any fancy wordplay, here’s the answer: press `:q` and it’s gone. You’re back to your editor.^([50](#chap35.xhtml_fn-q_is_not_quit))

Okay, so, like we did earlier, let’s start the help program up again and see what we can do with it. When you type `:h` you should notice that there are a bunch of words that are highlighted, like *links* from one part of the text to another, *hyper-links*, if you will. You’re right, that’s exactly what they are. Position your cursor on one of those links and type `<ctrl>]` to jump to the section referenced by that link. In reality, the help viewer is just showing you a specially formatted text file, coloring and centering and linking things according to the arcane rules of vim help files. If you ever write a vim plugin you would do well to learn this language, but for now we’re going to ignore it. The other half of the help magic is that it’s opening a new *window*, a concept that we’ll cover [soon enough](#chap21.xhtml_windows). For now all you need to know is that you can jump from window to another by typing `<ctrl>w` and a direction. Since the help window opens above your editor window you type `<ctrl>w j` and your cursor will jump down to your editor window. Type `<ctrl>w k` and you’re back in the help window.

### Getting the Help You Need

Vim’s help system can only be *helpful* if you know how to ask it for things. The maintainers of the vim docs have thoughtfully separated out the help topics based on the *mode* in which you can use them, and vim makes it easy to search in this way. I could include a list of the prefixes you need to use to view the various sections of the help docs, but why reinvent the wheel? Vim can do that all by itself; in fact, if you moved around a bit when you were looking at the help documents earlier you probably already saw the document we’re looking for.

If not, let’s go to the documentation now. In normal mode hit `:h` and find the line that says “get specific help” and place your cursor on that line. Now type `[zt](#zoom)` and you should see *exactly* what we’re looking for: A list of the prefixes you can use to view commands in insert mode, visual mode, options, and all the rest. Let’s look up an insert mode command, just because we can. The help search function isn’t case sensitive; so you can type everything lowercase and it’ll work just fine. Let’s look up `<ctrl>-r` because that’s an insert mode function that has a lot of functionality. In normal mode just type

```
1 :h i_ctrl-r
```

And you’ve got some useful information about how to use [registers](#chap14.xhtml_registers) in insert mode. Hit `ZZ` to close the help window and let’s keep playing!

### Relatively Shallow Secrets of the Help System

It shouldn’t surprise you that the vim help files are just a collection of plain text files^([51](#chap35.xhtml_fn-nosurprise)). When you type `:h [something]` what you’re doing is firing up vim’s built in help file search engine. It doesn’t (by default) do a full text search; it searches according to the specially formatted tags at the head of each section. But you can use it in other ways as well.

For example, you can search for a vim help file using its full name. Go ahead and type `:h insert.txt` and you’ll see the full insert mode help document, with it’s own table of contents and everything. It’s worth noting that *sometimes* you can search for things without the extension and end up in the same place. For example, if you enter `:h cmdline` you’ll get the `cmdline.txt` file, just as if you’d typed `h:cmdline.txt`. However, try the same thing with “insert” and you’ll get different results. Go ahead and try it: type `:h insert` without the `.txt` extension, and you’ll still end up in the insert mode help file, but instead of being put at the table of contents you’ll end up in “chapter 8: Insert mode commands”. This is usually what you want when you’re just looking for help on “insert”, but it illustrates the point: if you search using the `.txt` file extension you’ll be take to the top of the file, if you search without a file extension you’ll be taken to what vim considers the best match for your search term.

The open nature of vim help files makes it easy for plugins to include their own help files, and most of them do. If you installed pathogen in the [Plugins](#chap11.xhtml_plugins) chapter you can type `:h pathogen<enter>` and see the help file for that plugin.

So this is all well and good. But what if you don’t *know* what you’re looking for? Not to worry. You can just type `:h` and the word you’re looking for, then instead of hitting `<enter>` press `<ctrl>d` and you’ll get a list of possible topics that match what you’ve entered so far. Once you’ve found something that looks like what you want you just finish typing the term and you’re on your way.

For example, let’s say you’re looking for help on the `yank` command, but you can’t remember what it’s called. You just know that it starts with a “y”. Okay, we can handle that. Type `:h y<ctrl>d` and vim will give you a list of topics that contain the letter y. Which is an insanely huge list. If you can remember the next vowel (that’s an “a” for those of you following along at home) you can narrow it down to the exact term you want.

Okay, that wasn’t the best example. But when you’re trying to search for the help file included with some of the punnishly-named plugins like “fugitive” and “pathogen” just remembering that you’re looking for “something about *git*” (and therefore typing `:h git<ctrl>d`) or “something that modifies *paths*” (and typing `:h path<ctrl>d`) will get you where you’re going surprisingly quickly.

## 17\. Doing Things at Vim Speed

I know I promised a lecture free book at the beginning of all of this, so in my defense I’m going to say that this isn’t a lecture. It’s an *explanation*. **Totally** different. Definitely not preaching here.

The question has been put to me, “How is ‘the vim way’ better than the ways I’m used to? Why is `:w` ‘better’ than `<ctrl>s`?”

It’s a reasonable question. And if you want to do things the way you’re used to you can easily use gvim or MacVim or any of the other graphical vim clones; they all tend to use the OS defaults so you don’t have to change your muscle memory at all.

So why learn a new way? The answer is one word: **Ergonomics**. The special keys on most keyboards are hard to use because they were tacked on to a standard typewriter keyboard when we started using computers. Thus they tend to slow you down when you have to start using them. Let’s look at the classic example mentioned above: `<ctrl>s` ^([52](#chap35.xhtml_fn-ctrl_cmd)) vs. `:e`. By sheer keystrokes `<ctrl>s` wins. It’s just two keys and a file is saved, whereas `:e` is:

1.  `<shift>`
2.  `;`
3.  `e`
4.  `<enter>`.

You have to hit **four different keys** instead of just two! That’s incredibly wasteful!

Except for one thing: all four keys are right in the middle of the keyboard where you can reach them without moving your hands, while the `<ctrl>` key is down in the special key ghetto, and makes you move your hands to reach it. If you have a command that takes more than one of those special keys you get to play keyboard twister so you can reach something like `<alt><ctrl>5`.

The mouse is even worse. Whenever you reach for the mouse you’re moving your hand at least six inches, then finding your cursor, positioning it on or between some characters, trying to eyeball the position, then reaching for some keyboard shortcuts (left hand only) to perform some action, then getting your hand back to the keyboard and re-finding your place before moving on.

And you, the amazing and talented person you are, you do this several dozen times every day, quickly and efficiently, often without noticing it. But the promise of vim is that *you no longer have to*.

While you may not consciously think about the time you spend reaching for special keys or the mouse, you are losing time, and more than that, at least a part of your brain is distracted from what you’re doing; you’re losing *context*. The whole point of the vim way is to let you “touch edit” your text^([53](#chap35.xhtml_fn-touch-edit)). To that end vim is based almost entirely on three special keys:

*   `<esc>`
*   `<ctrl>`
*   `:`

Pretty much everything else you do in vim will be a regular ol’ letter or number key. While you’re using vim you can almost totally ignore the denizens of special key ghetto. You can just keep your fingers on home row without ever moving your hands from their resting position on the keyboard.

Now, you’re looking and have realized that `<esc>` and `<ctrl>` aren’t exactly ergonomically placed keys. Many others have realized this as well. The next chapter will go into a little more detail about how to fix this problem, but here’s a sneak preview: [remap the caps lock key](#chap19.xhtml_clmd) to be an extra `<ctrl>` key. Once you do that you’ve removed any need to move your hands down to the bottom row, which just slows you down. Also, vim interprets `<ctrl>[` as `<esc>`, and once you know that you never have to reach for that insanely placed `<esc>` button again. Your hands are now free to always hover right over home row, regardless of what you have to do in your editing, and you no longer have to break the physical or mental context you’ve built up while working.

None of this is intended to say that you must never use any other editor again. Even while writing this book I’ve used Scrivener, Multimarkdown Composer, Sublime Text and Ulysses in addition to vim, depending on what I was doing and where I was in the writing and editing process. You should always use the right tool for the job. But with a little practice you’ll find that vim becomes the right tool for most text editing jobs. ^([54](#chap35.xhtml_fn-Quickcursor))

## 18. Mapping Keys

One of the good things about vim is that it has a *lot* of commands, and pretty much every [plugin](#chap11.xhtml_plugins) brings a bunch more. One of the bad things about vim is that it has a *lot* of *hard to type* commands, and pretty much every plugin brings a bunch more. Fortunately, it’s easy to create keyboard shortcuts (or “key maps” in the vernacular) for these commands, thus freeing up your brain space and cutting down what you have to type into just a few characters.

However, this is definitely a topic where the Spider-Man warning applies^([55](#chap35.xhtml_fn-spiderMan)), because you can get yourself into trouble changing too much without thinking ahead. We’re going to go over some common-sense strategies for mapping keys in vim, and set up a few maps that will help you work faster and more happily. Adding a new key map in vim is a matter of adding a single line to `.vimrc`, and once you get used to the syntax it’s not terribly difficult. The problem is the syntax. Like many things in vim, it’s concise, compact, and aggressively opaque unless someone tells you how to use it. That’s why I’m here!

### All the Key map Commands

Since vim is a modal editor, it allows you to create key maps for each mode individually. The upshot is that you could have (this is **just an example**. Don’t do this) `<ctrl>s` mean “save” in normal mode, “search” in insert mode, and “select all” in visual mode ^([56](#chap35.xhtml_fn-butdont)).

You specify the target mode for your key map with the first letter of the `map` command:

*   **nmap** : normal mode
*   **vmap** : visual mode
*   **imap** : insert mode

Let’s take a look at how you would use these in real life.

The pattern for new mappings is *map-mode* *keys* *command*. Let’s say that you want to *always* append text to the end of a word when you jump to the end of a word. In stock vim you jump to the end of a word by just pressing `e` in normal mode. To enter insert mode we would add this line to `.vimrc`:

```
1 nmap e ea
```

And then either restart vim or do our old `:so %` trick to reload our settings immediately. Now, when you press `e` your cursor jumps to the end of the word and enters insert mode, all at once. But let’s say we didn’t want to overwrite a built-in vim command (smart move! But more on that soon). Let’s say we want to turn `<ctrl>e` into our “jump to the end and append” command. In that case we need to let vim know that we’re using `<ctrl>` in our keymap, and to do that, we wrap the keys we’re going to press in angle brackets, like so:

```
1 nmap <C-e> ea
```

In vim, putting the letter C with a dash and any other character inside angle brackets says “I’ll hold down Ctrl and this other character at the same time”^([57](#chap35.xhtml_fn-mappingAlt)). If you just typed

```
1 nmap C-e ea
```

You would have to type an uppercase C, a dash, and a lowercase e in that order to activate the key map.

Okay, so, we’ve got the basic idea of keymaps: Tell vim where to use our new shortcut, what the shortcut is, and what it should do. Simple, right? Right. But we’re not going to leave it that way for long. Normal mode is a busy place, and there are very few keys on the keyboard you can map with impunity. Fortunately, Vim has provided a way for us to extend the number of keys we can use without stepping on any currently mapped commands, using the `<Leader>` key.

### Take me to your `<Leader>` Key!

You’re right, if you look at any keyboard you won’t find a key with “leader” written on it. This is because vim allows you to decide what key you want to use as a preface to your custom keymaps. In our example above we mapped `<C-e>` to a command, but that’s already got a function in vim. What we could have done is written our mapping like this

```
1 nmap <Leader>e ea
```

And all we have to do is press… something and then e and we’re good! But what the heck is `<Leader>`?

By default, `<Leader>` is mapped to backslash (`\`). For most people this is a super annoying key to press and makes your “shortcuts” irritating. So for years people have added the following line to `.vimrc`:

```
1 let mapleader=","
```

Which sets the comma key as `<Leader>`. Once you’ve done that you can just press `,e` and you have a simple way to jump to the end of a word and edit it all at once^([58](#chap35.xhtml_fn-justasquick)).

If you forget what keys you have mapped you can type `:map` in normal mode and be utterly overwhelmed with text. We’ll get back to that in a while. For now let’s talk about things we *shouldn’t* map.

### What not to map

Vim being what it is, you’re free to map any function you like to any keyboard action you like, and make vim work exactly the way you’ve always wanted. You could decide that you don’t like `h j k l` and map them to some keys you like better, like, say, `w a s d`. But as my dad always told me when I was growing up:

> Just because you can doesn’t mean you should.
> 
> –*Nate’s Dad*

There are a few excellent reasons why you *shouldn’t* remap any of the basic commands. The first one is what I call the *wallpaper effect*^([59](#chap35.xhtml_fn-wallpaper)). As we have already stated, just about every key on the keyboard has a pre-defined job in normal mode. Let’s stick with the terribly bad example above and say that you want to remap the movement keys `h j k l` (because those are hard to remember) to `w a s d` (because you’re a gamer and use those all the time) . But if you do that you’ve got to figure out what to do about the following four commands:

*   Next word (**w**)
*   Append (**a**)
*   Substitute character (**s**)
*   Delete (**d**)

You could map them over to `h j k l`, but what sense does that make? `w` for “next word” is an natural and well crafted mnemonic. `k` makes far less sense. So you could try to map “Next word” to `n`, but then you’ve got to find a place for “find next”, and so forth.

Which leads to the problem of *portability*. One of the main reasons for learning vim is that it’s installed by default on just about every non-Windows computer ever, and once you know how to use vim you can use it edit files quickly over any SSH connection, or hop on anyone else’s machine and be productive almost immediately. But while *vim* is everywhere, your `.vimrc` file is only on your machines. This means that any time you connect to a computer that you don’t own you’re going to be trying to remember how to use vim the regular way all over again. Your muscle memory is going to trip you up, because you’ll be reaching for your custom keys instead of the standard ones. You could just get in the habit of hauling your `.vimrc` file everywhere you ever work, but this slows you down.

The other side of that is having other people collaborate with you via SSH or using tmux. Any vim users will be instantly and inconsolably furious when all the keystrokes they try do the entirely wrong things. It’d be like when you try to use someone’s Dvorak keyboard when you’re used to QWERTY or vice versa.

In general, you should approach any remapping of built-in, standard commands with caution. *Adding* a keymap for something you do regularly is probably not terrible, but it still makes you reliant on being at your own personal terminal. *Overwriting* a keymap for a standard function should only be done if you know there is no better option.

### What to Map

So what do you map? It seems like my advice is to leave vim in a pristine state, unchanged and trusting blindly in the wisdom of Bram and crew.

Well, not entirely. There are a lot of things that you should map, things that make vim more useful without crippling you on other machines. Most of these, unsurprisingly, have to do with plugins. Plugins are awesome. They extend your functionality and have become the core of any good text editor. And when you add them to vim it makes sense to find the most useful parts of the plugin and map those functions to something you like.

For example, let’s take the [fugitive](https://github.com/tpope/vim-fugitive) plugin by Tim Pope. Fugitive is a git management plugin, and exposes a lot of its functionality through the `:Gstatus` command. You could just type `:Gstatus` from the command line every time you wanted to use this plugin, or you could give it a nice, memorable keymap. Let’s choose the second option. Since this is a git plugin, the letter g seems appropriate, but we don’t want to overwrite it’s current functionality. `<Leader>` to the rescue! We’ll add the following to `.vimrc`

```
1 nmap <Leader>g :Gstatus<CR>
```

And now (if you’ve remapped leader to the comma key) we can just press `,g` and get all that git status goodness in two characters, and we did it all without harming vim’s central functionality.

The other benefit here is that you can go to vim on any other machine and do your work without having compromised your muscle memory for the basics. Chances are that if you’re working on someone else’s computer you’re not using git, because…that just feels wrong somehow. You’d be signed in as them and your commit would show up under their name…it’s like wearing someone else’s underwear. And on that pleasant note let’s talk about a useful, nay *essential* keymap that has to be done *outside* of vim itself.

### `<Plug>`

Okay, so there’s one more not-on-the-keyboard key that we have to deal with. Unlike `<Leader>`, you’ll never have to map a key to `<Plug>`, but you’ll see it come up from time to time, so we’re going to go over it in a high-level fashion.

Without getting into the details, `<Plug>` is a way for plugins to make it easy for you to create shortcuts for their functions. For example, let’s say you have a plugin with an awesome feature called `awesome_feature`. The plugin developer could add the following to their plugin:

```
1 noremap <unique> <Plug>awesome :awesome_feature <CR>
```

And then you could map that to something you want by adding this to `.vimrc`:

```
1 nmap <Leader>a <Plug>awesome
```

To use their awesome feature from there on out.

### Recursive Mappings, and How to Avoid Them

One feature of vim keymaps is that they can include *other* keymaps that are recursively executed. Like any feature, this can be used poorly, or used well.

#### Terrible Keymap Recursion

Let’s consider the case of “Bob”, a person who exists entirely to make poor choices in examples.

Bob decides that he wants to use `F2` to copy a line. So he adds this line to `.vimrc`:

```
1 map <F2> yy
```

Bob is forgetting that you shouldn’t remap standard commands, but that’s because he hasn’t read this book yet. Someone buy him a copy, quick! But as bad as this idea is, it still works; bob can now press F2 instead of typing `yy` to copy entire lines, if that’s your idea of a good time. But he’s not done yet!

Bob (who is a huge Star Wars fan) is writing the seminal work on Wookiee culture, and wants to create an abbreviation for the name of the Wookiee home world, Kashyyyk. Bob is also a huge fan of overly fancy mappings, so he creates the following abbreviation:

```
1 abbr kk Kash<F2>yk
```

Can you guess what will happen when Bob types `kk` in his editor? That’s right, he’ll get the actual word Kashyyyk, because vim treats the characters and keymaps in abbreviations as if you entered them yourself, and pressing `F2` in Bob’s world gives you `yy`. Bob is to be congratulated for making his keymap totally gaudy, terrible, hard to read *and* two characters longer than it has to be.

But Bob still isn’t done doing stupid things! He really **really** likes the letter `y`, so he’s going to modify his `F2` keymap like so:

```
1 map <F2>y<F2>
```

So now when Bob presses `F2` vim will type the `y` character, then see the `F2` key, which tells it to type y and then the `F2` key…and so on, forever. Or until Bob presses `Ctrl-C` to kill the recursion. This will also turn his `kk` abbreviation put an infinite number of `y`s in the middle of Chewie’s home world.

The point of all this is that recursive key maps are totally possible in vim, and you can use them more intelligently than Bob does. But even Bob’s terrible use of recursion shows us a few useful things:

*   If you include a keymap inside another keymap you can change the underlying map and it will update the outer one as well. ^([60](#chap35.xhtml_fn-rewrites))
*   Infinite recursion is entirely possible, but getting out of that state is fairly easy.

#### A More Useful Example

So let’s take the lessons we learned from Bob and use them more intelligently. Let’s start with something you might actually want to map:

```
1 imap <F5> <C-R>=strftime("%H:%M")<CR>
```

Don’t worry too much about that command (but if you want to know more you can check out [the vim wiki](http://vim.wikia.com/wiki/Insert_current_date_or_time)). It inserts the current time in “hour:minute” format. So if I pressed `F5` right now it would put “12:58” right before my cursor position.

Now let’s say we want a simple abbreviation to write log entries. We would add another line like this to `.vimrc`

```
1 iabbr logt <F5>:Entry
```

And now when we’re typing in the log we can just type `logt` and a timestamped log entry will be created. Now let’s say we want to change the timestamp format. All we have to change is our `imap` line:

```
1 imap <F5> <C-R>=strftime("%c")<CR>
```

And our log entry goes from

```
1 12:58: Entry
```

To

```
1 Sat Jun 29 12:58:32 2013: Entry
```

#### Avoiding Recursion Altogether

But they can also be somewhat confusing when you create a keymap that recurses into another keymap that you didn’t want or expect. Fortunately you can easily tell a keymap that you *don’t* want it to parse any keymap it comes across and just type the characters you typed, thank you very much. To do this you just change your map from this:

```
1 imap <Leader> d dd
```

To this:

```
1 inoremap <Leader> d dd
```

This is true of all the other modes as well: `vnoremap`, `nnoremap` work in exactly the same way. As you probably guessed, the `nore` stands for “no recursion”, and ensures that anything in the expansion side of the remap is left un-evaluated. In general, it’s a recommended practice to use the no recursion versions, because they’re “protected” against accidental remaps from new plugins or other keymaps you may add later.

## 19. Fancy Insert Mode Tricks

Back in the chapter about [Modes](#chap10.xhtml_modes) I mentioned that insert mode is fairly light on commands, because that’s the mode where you’re supposed to be, you know, *inserting* stuff. But “light on commands” is definitely relative, as there are a *lot* of things that you can do in insert mode, once you find out about them. That’s where I come in. I guess I could also mention that vim’s built-in help system has a lot to say on the subject: just type `:h insert.txt` to find out more. And by “more” I mean “**everything**” The help system is thorough, to say the least.

In the [last section](#chap19.xhtml_mapping-keys) I briefly mentioned the fact that vim uses the `<ctrl>` key for just about everything. This is especially true in insert mode, where all the regular keys are doing their regular stuff. Vim uses the `<ctrl>` key to give you access to useful functions such as the following:

| Command | result |
| —— | —— |
| `<ctrl>w` | Delete the *word* before the cursor |
| `<ctrl>u` | Delete the *line* before the cursor. |
| `<ctrl>t` | *Increase* line indent by `shiftwidth`^([61](#chap35.xhtml_fn-shiftwidth)) |
| `<ctrl>d` | *Decrease* the line indent by shift width |
| `<ctrl>n` | Find next completion suggestion |
| `<ctrl>x` | Hoo boy. I’ll get to `^x` in a moment. |
| `<ctrl>r` | Insert the contents of a register. More on what that means soon. |

### `<ctrl>x` Adventures

Technically, `<ctrl>x` moves you into a sub-mode called, appropriately, “CTRL-X” mode. Most of the commands available in this mode are *completion* commands; vim’s version of autocomplete. We’re going to play around with some of these, but CTRL-X mode isn’t the purview of a “painless” book like this one. Instead of diving too deeply I’m going to refer you to some experts on the subject.

For now, though, let’s play with a couple of simple commands in CTRL-X mode. The first one is the awesome-sounding “omni complete” which you access by typing `<ctrl>x <ctrl>o`.

### `<ctrl>r` Funtimes

The `<ctrl>r` command gives you an easy way to paste in information from any of your [registers](#chap14.xhtml_registers). Just type `<ctrl>r` and the name of the register you want to paste in. So `<ctrl>r a` gives you the contents of `"a` right where your cursor is sitting. In essence all this does is save you a trip back to normal mode.

For the most part this is a simple concept, and we mostly covered it in the chapter on registers. But `<ctrl>r` has a few other tricks up its sleeves. Well, okay, one other trick that we’re going to play with here, which is pasting from the *expression register*.

The expression register is pretty much what it sounds like: you can give it an expression and when you paste it it gives you the result of that expression. What’s even better is that vim will let you do both in a single step, all from within insert mode. All you have to do is type `<ctrl>r=` and the expression you want to evaluate. You can do simple expressions like `<ctrl>r=40+2` and it’ll drop the expected result right where your cursor is sitting. But wait, there’s more! (There’s always more.) The expression register doesn’t just deal with *mathematical* expressions. You can also have it deal with *programmatic* expressions!

But not in this book. Expressions are powerful and interesting, but certainly not painless. So instead I’m going to point you at some [other resources](#chap30.xhtml_more-expressions) to check out if you want to enhance your expression knowledge.

### Completions!

This is one of those places where vim tries hard, bless its heart, but it’s not the best. I realize that saying that will get me skewered by people who know vim far better than I do, but here’s the skinny.

Vim looks through the open files and finds words that you’ve written, making up a nice index. When you press `<ctrl>n` in insert mode it does it’s best to figure out what word you have already entered in the document that you might be typing again. If there’s more than one possibility it’ll give you a list of all potential matches. Press `<ctrl>n` again to go down to each new item in the list, and then start typing again when you’ve found the item that you want.

This is super-helpful when you have variables or methods with long names that you have to enter over and over again. Usually you can type the first few letters and then just hit `<ctrl>n` to finish it. This is another way to help sanitize your code. Dynamic languages like JavaScript have no problem inventing a new variable on the fly if you happen to spell your current variable wrong once or twice, through no fault of your own. If you always use the completion function to put your variable names into code after the first time you can be assured that you’re spelling it the same way each time.

Like I said a second ago, Completions are one place where other editors (and here I’m talking specifically about Sublime Text, but frankly Visual Studio is also great at this) have eclipsed vim (Eclipse is pretty bad at it, though; for the most part). However, one tiny rough patch amidst all the goodness of vim is hardly worth considering, right?

## 20. Vim Windows Are Not Microsoft Windows

Okay, it’s time to see just how not-scary vim’s help system really is. The problem most first-time vim-trier-outers have is that they type `:help` and then the screen is split in half and they have no real way to jump from the help text back to the editor. If you’re feeling adventurous you might try `:q` and notice that you can kill the help window, but you’re still kind of at it’s mercy. Let’s talk about how vim windows work and how much of a non-issue they are.

Note that in this chapter I’m going to start putting the command to look at the corresponding section in the official vim documentation. It might be super helpful. We’ll see.

### Opening and Closing Windows `:h opening-window`

We already mentioned how you can get *rid* of a window: just “quit” it with the `:q` command (remember, `ZZ` and `ZQ` work just as well). But what if you *want* a new window? That’s easy too. You can “split” your current editor window into two windows with the `:sp` command. When you do this you’ll see that both windows are viewing the same file ^([62](#chap35.xhtml_fn-file-buffer-redux)). The thing is that you can change the file being edited in either window with all the usual commands: `:e` works just fine, and if you installed NERDTree in the plugins chapter then the NERDTree will let you navigate and edit files in whichever window was most recently in use. As you’ve probably guessed, NERDTree itself opens a long tall window.

Which leads to more interesting possibilities: can you open windows that are different shapes and sizes? Can you change the size of an already opened window? The answers to your questions are yes and yes, but we’ll get there in a moment. For now we need to look at how you jump from one window to the other.

### Window Commands begin with `<ctrl>w`

Pretty much everything you want to do with a window other than opening or closing it can be done by pressing `<ctrl>w` and then entering your desired command. The obvious mnemonic for this command is “control windows!”, something Microsoft has been trying to do for years^([63](#chap35.xhtml_fn-rimshot)).

You could probably say that `<ctrl>w` enters a new mode called “window command mode” but that’s not an official name. And anyway we already did the modes chapter.

### Moving Between Windows `:h window-move-cursor`

Armed with this new knowledge let’s look at some of the things you can do in window command mode^([64](#chap35.xhtml_fn-wcm)). The first one is jumping between your open windows. To do this you simply press `<ctrl>w` to enter window command mode and then use your movement keys to jump from one window to the next. So `<ctrl>wk` will move you one window up, `<ctrl>wj` will move you one window down, as you would expect. You can figure out how to move from side to side.

It is that simple, and yes, smartypants, you can put counts in the middle there too. If you have three windows stacked up like pancakes and you want to get from the bottom pancake to the top pancake you can use `<ctrl>w 2k` to jump straight to the top window. Or Pancake. Whichever you want. For the record, if you have three windows stacked up and you enter `<ctrl>w 15k’ it’ won’t wrap around five times; it’ll just go to the top window and tacitly ignore the fact that you told it to do something stupid. Vim is thoughtful like that.

### Resizing Windows `h: window-resize`

There are a *lot* of ways to resize windows, which give you varying degrees of ease and control. Let’s start simple. By default, when you create a new window vim will split your current window into even sections. If you want to resize that window you’ve got a choice to make: do you want to make it taller, shorter, wider, or thinner? Depending on how you split out your windows some of these may not be relevant; if you’ve split the entire screen into two horizontal windows, for example, you can’t make your window wider or narrower; it’s stuck at 100% width. But you can make it taller or shorter, so let’s do that first.

To make a window taller you type `<ctrl>w +`. In this case that `+` is an actual plus sign, because you’re *adding* a line to the window. You can add several lines by specifying the count between `<ctrl>w` and the plus, like so: `<ctrl>w 4+`.

to make a window shorter you can do the same thing, only with a dash: `-` instead of a plus sign. So, it’s a *minus* sign, see? `<ctrl>w -` gives you a window that is one line shorter; the count trick works as well: `<ctrl>w 4-` will make the window four lines shorter.

If you have been changing window sizes somewhat haphazardly and want to go back to having them all be the same size you can pull that off by typing `<ctrl>w =`. The mnemonic here should be obvious.

Okay, so making windows taller or shorter is obvious, what about making them wider or skinnier? It’s also pretty straightforward. You type `<ctrl>w >` to make the window *wider* (think of it as pushing the right side of the window out farther). To make it *thinner* you do the opposite: `<ctrl>w <`. Again, you can use counts in the middle of both of these commands.

So, let’s sum up: to change the sizes of windows, you start out with the *Windows Command Mode Entry Access Key* (`<ctrl>w`) and press one of the following to change the window:

*   `+`: Make the window **taller**
*   `-`: Make the window **shorter**
*   `>`: Make the window **wider**
*   `<`: Make the window **narrower**

We’ll play with these commands in `windows.txt`, the special word document designed just for window funtimes.

### Moving Windows Around `:h window-moving`

This is not something I use all that often, but it can come in handy from time to time. Let’s say that you were working on a file, and you opened the help documentation. By default it opens *above* your current window. Let’s say you want to keep the help window open, but you prefer having your code window on the top. To move your current window (remember, when you open a help window your cursor jumps to it, and it becomes your current window) to the bottom all you have to do is press `<ctrl>w J` (that is an uppercase `J`) to send that window to the bottom of your screen. Move it to the top of your screen with `<ctrl>w K`, as you would expect.

Most of the time these are the only window moving commands you’ll need, because you’ll probably only ever have two vim windows open. But maybe you’re one of *those* people who have all kinds of windows open all the time. If you have *lots* of windows open and want to do some less drastic jumps then read on. Everyone else can just go to the [next chapter](#chap22.xhtml_tab-pages).

#### Making Windows Dance

The following commands are only useful if you have three or more windows open. I don’t know why you *would* have three or more windows open, but I’m not here to judge. Maybe you’ve got a huge monitor and a better brain than I have, so you can focus on three or more things. Whatever. Here we go.

You can **rotate** windows using `<ctrl>w r` and `<ctrl>w R`. The lowercase version rotates windows *down*, meaning the top window becomes the second window, second becomes the third, and so on. The bottom window jumps to the top. When you move everybody around your cursor stays in the window you were in when you started the little dance.

The uppercase version of the command goes the other way; the top window jumps to the bottom, the second-to-the-top window becomes the top window, etc. Both versions of this command take a count as well, so that it will spin the window wheel by *N* steps instead of just one.

If you just want to swap two windows, but want to leave all your other windows alone you can use `<ctrl>w x`. Let’s say you have the following layout:

```
1 +-------------+
2 |      1      |
3 +-------------+
4 |      2      |
5 +-------------+
6 |      3      |
7 +-------------+
```

And you want to trade 1 and 2 but leave three on the bottom. You just hit `<ctrl>w x` and you now have:

```
1 +-------------+
2 |      2      |
3 +-------------+
4 |      1      |
5 +-------------+
6 |      3      |
7 +-------------+
```

If you give this command a count *N* it will trade your current window with window *N* and leave everyone else where they are. You can use this to swap windows 1 and 3 while leaving window 2 happy right in the middle. Vim numbers the windows like a human would, so the topmost window is window 1, not window 0 like you would expect from a programmer-based editor.

In any case, if you have your cursor in window 1 and you hit `<ctrl>w 3 x` you will get

```
1 +-------------+
2 |      3      |
3 +-------------+
4 |      2      |
5 +-------------+
6 |      1      |
7 +-------------+
```

If that’s your idea of a good time. Unlike the window rotation commands, the window swapping command will move your cursor to the new window. Put another way, when you swap windows 1 and 3 your cursor will stay in the topmost window, but the windows will move. Look, just try it a few times, It’s pretty natural.

## 21. Tab Pages Are Not Browser Tabs

One of the more useful features in just about any app is the ability to have multiple tabs open, looking at multiple files or web pages or whatever. And vim has that too! But it’s not exactly what you think it is, and until you get used to how vim thinks about tabs it’s going to seem weird, hostile, possibly even *aggressive*. But in reality vim just wants to help you out; it wants to do whats best for *you*, if you would just let it. Vim worries.

Okay, Let’s get into this. In a browser, a “tab” is your view of a single web page. If you want to view multiple tabs in a single window you open multiple tabs. And here is where we get into linguistic trouble. We’ll get more into the business of vim terminology in the [next interlude](#chap23.xhtml_interlude-3), but let’s skim through it right now.

These days, when we say you have a window open on your desktop (one of my favorite mixed metaphors in all of computing lingo) we are talking about the graphical user interface your OS uses. When you open a browser, or a modern IDE like Sublime Text or IntelliJ or even Visual Studio, you can have multiple *tabs* inside a single *window*. Vim, on the other hand, allows you to put multiple *windows* in a single *tab page*. And people get hung up on this.

You certainly can use vim tab pages the same way you use tabs in other programs: just open a single window in each tab. But to limit yourself like this is to miss out on the power of tab pages. A vim tab page can have as many windows as you want, laid out however you want, independent of any other tab page you’ve got open. So you can have two tall side-by-side windows in one tab page, and three horizontally divided windows in another tab page. You’ve got a lot of freedom to do things your way.

### How To Use Tab Pages `:h tabpage`

Okay, enough lecture. Tab pages are simple to use, once you know they exist. To create a new tab you just type `:tabnew` and a new tab will open. If you want to open a new tab with a specific file you just include the file name: `:tabnew file.txt`.

Once you’ve created the new tab you can split it up into windows just like you’ve been doing this whole time. Each tab acts just like a full version of vim.

For one reason or another, tabs are a place where vim *explodes* with redundant ways to do the same thing. I always prefer the shortest method of accomplishing a goal, so I will list those first, with the other possible methods listed for good measure.

*   Opening a new tab:
    *   `:tabnew` *filename*
    *   `:tabe` *filename*
*   Close current tab
    *   `:tabc`
        *   `:tabclose`
        *   Note that both of the above methods can take a `!` to force the tab to close even if there are unsaved changes in a buffer.
*   Close *all* tabs:
    *   `:qa` (will fail if there are unsaved changes)
    *   `:qa!` (force-close all tabs)
*   Close other tabs
    *   `:tabo` Close all other tabs.
*   Go to the next tab - `gt` - `:tabn`
*   Go to the previous tab - `gT` - `:tabp`
*   Go to a specific tab - `:tabfir` goes to the **first** tab - `:tabl` goes to the **last** tab - *tabNumber*`gt` Goes to the tab number given - *tabNumber*`gT` Goes to the tab number given
*   Reorder tabs - `:tabm`*number* places a tab **after** the given tab number. Use 0 to make the current tab first. - `:tabm +`*number* move a tab *number* places **right** - `:tabm -`*number* move the tab *number* places **left**
*   List all open tabs - `:tabs`

I’d like to say more about this topic, but it’s pretty straightforward. If you like tabs you should play around with this stuff. If you’re happy doing everything in one tab then you can safely ignore this stuff. But it’s easy to use and when you do it in the terminal you look like one of the truly awesome uber-nerds. Almost as cool as someone who uses [tmux](http://tmux.sourceforge.net/), but that’s a topic for another book ^([65](#chap35.xhtml_fn-another_book)).

## 22. Interlude: Reviewing Views

It’s worth taking a few moments here to go back over the hierarchy of things that show up in a vim session, just to get them all straight in our minds and to take a breather. The quick rundown looks like this:

1.  A *file* is a bunch of data on a disk.
2.  When you tell vim to edit a file, it creates a *buffer* of all the data from that file and lets you edit that.
3.  A *window* lets you view the text in a buffer. You can have multiple windows open to different parts of the same buffer, if you so desire, or you can have multiple windows looking at different buffers on the same screen.
4.  A *tab* (or, more accurately, *tab page*) is a collection of all the windows you can see at the same time. You can have a bunch of tabs open, and it’s super simple to switch between them.

Let’s work from the bottom up, and just for fun we’ll do this in a semi-Q&A format.

### Files

**Q:** So, vim doesn’t edit files?

**A:** No. When you open a file in vim it is copied into a *buffer*, which is what you edit. Interestingly, the buffer is saved off at intervals into a *swap file*, which is there to keep you from losing your work. But we’re going to ignore that for a minute. Vim’s buffer is entirely in memory, and is only written back to the actual disk when you give vim the `:write` command.

**Q:** Can you have multiple buffers for the same file?

**A:** Vim works hard to prevent this from happening. When vim opens a file it creates the aforementioned swap file. If you open another copy of vim and tell it to edit the same file it will see the existing swap file and get very nervous. Before it lets you start editing the file it will ask if you want to make a copy, or perhaps open the file in read-only mode, basically do anything *other* than have two copies of vim fighting over the swap file. Having multiple authors on a single file is a task best handled by software specifically designed with that in mind, and vim isn’t that software.

When you save a document vim copies the contents of the swap file into the current file. When you close vim it deletes the swap file. I cover this in a little more detail in the [next chapter](#chap24.xhtml_files-vs-buffers) so you can skip ahead if you like.

**Q:** So why does the swap file even exist?

**A:** Because things don’t always happen perfectly. The swap file exists for occasions where vim (or your computer) crashes without saving the changes you made to the buffer back into the file. Which is part of why you only have one swap file per file: it keeps the history clean and makes it easy to restore your changes.

That said, you can have more than one view into the same buffer, by having that buffer open in multiple *windows*.

### Windows

**Q:** What’s the difference between a buffer and a window?

**A:** That’s easier to show than tell. Do the following:

1.  Open vim without specifying a file.
2.  Type `:sp` to split your screen into two windows
3.  Start typing in either window.

You should see your text showing up in the other window. Both windows are looking at the same buffer, so your changes are reflected in both places. Having multiple windows into a single buffer is useful for reasons other than boring party tricks. You can have one window showing a method you’re referencing and the other showing the method you’re writing, for example. But windows are usually better used when they’re looking at different buffers.

**Q:** How many windows can you have on a screen at once?

**A:** That depends on how big your screen is. If you have more than three open I suggest opening a new *tab*.

### Tabs

**Q:** Okay then, how many *tabs* can I have open at once?

**A:** By default you can have ten tabs. I don’t know why. I *also* don’t know why you would want to *change* this number, but if you’re so inclined you can add a statement like `set tabpagemax=15` to your `.vimrc` file and then you can have 15 tabs open. It’s up to you. If you’re working on 15 sets of files at once then you’re far better at multitasking than I am.

**Q:** Why did you make a huge deal about the difference between *tabs* and *tabpages* earlier, but now you’re just calling them all *tabs*?

**A:** Because *tab* is way shorter than *tabpage*, both to type and to say. Once you got the idea that you weren’t getting a one-tab-to-one-file correspondence like you’re probably used to from your browser we could settle down and simplify the language. It’s true, however, that a lot of people will still use vim to open a tab for every file they’re editing, and that’s fine. I just wanted to remind you that you can do more with a vim tab than you can with a browser tab.

**Q:** Is there an easy way to open all the files you’re working on in separate tabs?

**A:** I don’t know about “easy” but if you want to open vim with a bunch of tabs you can call it like so:

```
1 vim -p file1 file2 file3
```

And you’ll have your files all in their own little tabs. I guess if you have a good programmatic way to build that command that would be “easy”, but I generally just use NERDTree to open files from within vim.

**Q:** Why are you so against using a tab for a single file –or *buffer*, if you insist– and so adamant that you need to have multiple windows open on each tab?

**A:** I’m not saying that you have to have multiple windows on each tab; I often use tabs for a single buffer. I just want people to remember that you’ve got more options and not get stuck thinking that one tab always equals one buffer.

The other pitfall comes with plugins like NERDTree. People get used to having their file explorer open on the side of the screen, and having it be persistent across all tabs. Vim doesn’t work like that. You can *make* it work like that with scripting and whatnot, but by default that’s not how things work in vimworld. Just remember that all the windows you can see exist on a tabpage, and you’ll be fine.

## 23. How Vim Thinks

This chapter has a few little odds and ends, useful bits of advice and insight into your new favorite editor. You can certainly read this chapter through, beginning to end, but the sections mostly stand on their own.

### You Don’t Edit *Files*, you Edit *Buffers*

This is nothing new: When you open a file in vim it creates a copy of the file in memory and all your changes are made to that copy. When you save the file your changes are all written back to disk. Pretty much every editor does that. But it’s worth knowing that a lot of vim terminology has to do with buffers. Okay, that’s the short answer. If you want more, keep on reading. If that’s good enough for you then we’re done here.

So, as I said, vim writes your changes to memory until you tell it to save them, because writing every character to the disk the moment you pressed it would be crazy slow and inefficient. So instead, vim waits until you’ve entered 200 characters, or sat around doing nothing for four seconds before writing anything to disk.

You see, when you open a file in vim, it creates a “swap” file that holds your changes while you edit. So if you’re editing the file `swap.txt` vim will create a hidden file called `.swap.txt.swp`. Once you start making changes vim will stash your changes away in this swap file whenever you’ve entered 200 characters or haven’t done anything for four seconds.

Why is vim doing this? Because it’s *got your back*, friend. If your computer crashes while you’re in the middle of a big project you’ll never lose more than 200 characters’ worth of work. When you re-open the file vim will notice that there’s a `.swp` file sitting around and ask if you want to recover your changes from that file. In most cases this will get you right back up to speed.

On the other hand, if you decide all the changes you’ve made during this editing session are pure garbage, you can just ditch them by typing `:q!` and the `.swp` file is destroyed, no questions asked. Nothing will be saved to your file at all.

### Updating Vim

Do the math: Vim is over twenty two years old, and is (at time of this writing) on version 7.4\. This means that you get a major vim upgrade once every 3.14 years. ^([66](#chap35.xhtml_fn-chrome)) You don’t need to worry about updates all that much.

But Bram and company are making improvements all the time, and it’s worth it to stay up to date with the latest and greatest, even if most of the patch-level updates aren’t going to rock your world. Depending on your OS the upgrade instructions are a little different.

Linux/Unix folk have the easiest time of it. Your system’s package manager will most likely always include the latest version of vim, so as long as you run regular updates you’ll be fine.

On Windows you pretty much just need to watch the website for announcements of new versions. If you’re using [Cygwin](http://cygwin.com/) to get your vim fix, you can use the Cygwin package manager which will keep you up to date. As with the linux people just run your package manager’s update functions every so often and you’re golden.

On OSX you’ve got two choices, both of them…okay. OSX does ship with a version of vim, but as of 10.8 it was version 7.3, when the current version is 7.4\. You can wait for Apple to update their system vim, or you can use [homebrew](http://brew.sh/). Getting up and running with homebrew is quick and easy, but beyond the scope of this book. For those who don’t know, homebrew is a package manager for OSX that builds open source projects on your system from source. Once you’ve got homebrew installed you can just type `brew install vim` and you’re up to date with the latest and greatest. To keep it up to date you need to *update* homebrew every once in a while (`brew update`), which gets the latest package information, and then *upgrade* your installed packages (`brew upgrade`). Do this once every couple of weeks and you’re in good shape.

In all cases you have the option of compiling vim yourself. You can set all manner of flags and options and compile things in or out of your vim install, but the process is definitely ***not*** painless, so I’m going to follow my usual pattern of pointing you to [a decent resource](http://vim.wikia.com/wiki/Building_Vim) on the topic and quietly move on to the next chapter.

## 24. Visual (Mode) Basics `:h visual-mode`

Visual Mode is simple and useful once you get into it, but it can take some getting into. This is partially because there are separate visual modes that have commonalities, but aren’t identical. Let’s cover the similarities first.

The whole point of visual mode is that it lets you select a block of text, well, *visually*, and apply an action to that block of text. There are a number of times where it can be a lot more intuitive to *see* what you’re going to change before you make the change. Let’s start with the most basic form of visual editing.

### Characterwise Visual Mode `:h characterwise-visual`

To enter this mode you simply press `v` in normal mode. As you probably guessed, it’s called “characterwise” because it lets you increase or decrease the size of your selected region one character at a time. Once you’re in this mode you can use all the standard movement keys to add or subtract from the selection.

As you might also suspect, you can start visual mode with a count before the `v`, like this: `5v`.

### Linewise Visual Mode `:h linewise-visual`

There are few surprises here. As you would expect, in *linewise* visual mode you can select entire lines instead of individual characters. This mode is useful when you want to grab a whole block of text all at once. You’ll be able to tell that you’re in linewise mode because the status board on the bottom will say `-- VISUAL LINE --` instead of just `-- VISUAL --`. As with characterwise visual, you can start linewise with a numerical argument and it will select that many lines: `5V` will select five lines, just as `5v` selects five characters.

### Blockwise Visual Mode `:h blockwise-visual`

In this mode you can select a *block* of text. Blocks are special: they can be expanded both *horizontally* (along a line) and *vertically* (across lines). There are a number of good reasons to use this functionality, but it does take more skill to handle than the other types of visual mode.

You enter blockmode with `ctrl+v`, and the status line will read `-- VISUAL BLOCK --` when you do it. Once you’re in visual block mode you can select a rectangular region with all the standard motions, searches, etc, just as with characterwise visual mode.

A common use for visual block mode is prepending something to a bunch of lines at once. Let’s say you’re writing javascript and you realize you wrote this:

```
1 function someThing(data){
2 	a = 1
3 	b = 2
4 	c = 3
5 	d = "hi bob"
6 	…
```

And you realize two things: one: your variable names are terrible, and two, you forgot to put a `var` before them, which will fail if you enable the `use strict` option on this file. Block mode can’t help you with the first problem, but your second problem is so common there is a special shortcut to fix it. Here’s how it works:

1.  Enter visual block mode with `<ctrl>v`
2.  Select the first column of each row by positioning your cursor before the first variable declaration and pressing `j` three times
3.  Type `I` (that’s a capital I, or `<shift>I`)
4.  Type `var`
5.  Press `Esc` (or `<ctrl>[`)

Vim will prepend your `var` declaration to each line you selected in visual block mode. Now go fix your variable names.

And before you ask, yes, you can use `A` in visual mode to *append* something to the end of each line in a block mode selection. There’s no way vim would forget something that fundamental. In fact there are a number of very intelligent and useful visual-block-only commands that make common programmer formatting tasks much easier. You can find a full list in the help topics by entering `:h blockwise-operators`, but I’m going to mention one more. Well, two more, but they’re mirror opposites, so it’s *basically* one more…

***ANYWAY***

when you’ve selected a region in visual block mode you can use `>` to indent the region by one “tab”^([67](#chap35.xhtml_fn-shift-width)) . Similarly, pressing `<` while in visual block mode “outdents”^([68](#chap35.xhtml_fn-outdent)) the entire region by one tab.

### Common Visual Mode Commands

Block mode’s Prepend feature is great, but there are a lot of other features that all the visual modes share. here’s a quick highlight list:

When you’re in a visual mode, you can use `o` to jump between the beginning and end of your selected region. This is helpful if you want to expand the selected region to include a few characters you missed at the beginning, then jump back to the end of the selection and grab a few more characters there.

In normal mode `gv` will re-select your previously selected area, which is useful if you…want to select the same area again. If you’ve recently done a search `gn` will highlight everything between your cursor and the next occurrence of the search term, while `gN` will select everything between your cursor and the *previous* occurrence, much like `n` and `N` move your cursor between occurrences of a search term.

Again, this is not a complete list. If you want to see *all* the commands and text objects you can use while in Visual mode you can check out the help document in vim by using `:h visual-operators`.

## 25\. Vim GUIs

There are a lot of good reasons to use vim from the terminal: it’s fast, light on your system, and when paired with tmux it lets you keep all your command line eggs in one basket. But there are good reasons to use the graphical versions of vim as well: they’ve usually got better system integration, buttons, tabs, and all the things you thought you were losing forever when you started on this vim adventure. Let’s spend a little time exploring the graphical side of vim.

There are (more or less) three different graphical versions of vim: `gvim`, MacVim, and Windows Vim. But all of them will start if you call `gvim` at the command line, so we’re going to call all of them “gvim” for the sake of simplicity. Installing them is beyond the scope of this book, because the process varies so much from system to system. A search engine is your friend in this case.

### Setting Expectations, Then Setting Some Settings

First off, let’s clarify what we mean when we say “graphical” vim. You’re not getting a full on IDE like IntelliJ or Visual Studio. In general what you get is system chrome around a regular vim session, and a few other perks. If you use tab pages they will be rendered as actual, clickable tabs, just like in an IDE. There can be a few buttons on the screen. You can play with menus, if that’s your thing. We’ll get to all these things in a minute. But first, let’s talk about settings.

Throughout this book I’ve been showing you changes you can make to your `.vimrc` file, the all-powerful settings file that tells vim how to behave. And if you want, you can just keep using that file to hold all of your gvim-specific settings. But there’s a better way. You see, when you start up `gvim` it *sources*^([69](#chap35.xhtml_fn-reads)) your `.vimrc` file first and then looks for a file called `.gvimrc`. If it finds that file it will source it as well. If you don’t have a `.gvimrc` file then it’s done. There are two benefits to this approach. The first is that you can keep your gvim settings all in one place and not have to wade through them when you’re working on your regular vim stuff. The second is that *vim* doesn’t have to wade through them when you’re just loading up terminal vim. The third (okay, there are three main benefits to this approach) benefit is that you can override settings from terminal vim when you run gvim.

If you don’t already have a `.gvimrc` file set up you can simply start editing it and put all your gui-specific stuff in the new file. And what kind of stuff would that be, you ask? You can find an exhaustive list of all options you can set by going into vim and typing `:h option-list` as you might expect. As you might also expect, this list will give you a slight headache^([70](#chap35.xhtml_fn-allday)) if you try to process it all at once. For our purposes you can do a search for the string `gui` to get to the options we’re thinking about now.

Most of these are things you won’t have to worry about directly, but there’s one that we all love: `guifont`.

### Setting the Font in `gvim`

In terminal vim you set your font in your terminal and it applies to everything that you do in that terminal. But if you want to set your font in gvim it’s a little different. I mean, sure you *could* just find a menu option that would allow you to set your font, but where’s the fun in that? I’m going to show you the way the cool kids set their gvim font in three easy steps.

#### Step 1: Use the Font Picker, Luke

Open up gvim and type

```
1 :set guifont=* 
```

on the command line. It should pop open your system’s font picker. MacVim will even be so kind as to choose the “monospaced” font group to give you the best code fonts. Choose the font you want, then close the font picker. You might think this would be the one and only step. You would be wrong, sadly.

#### Step 2: Find out What Vim Thinks Your Font Is Called

Vim uses vimscript, an archaic language that uses a few non-intuitive conventions. Instead of figuring out how to tell vim what font you want by trial and error you can type

```
1 :set guifont?
```

And it will tell you what font you’re currently using. My gvim at the moment would say

```
1 Andale Mono:h14
```

The `h14` part, as you might expect, is the size in points. Or `h`, apparently.

#### Step 3: Set the font in `.gvimrc`

Okay, so now all you have to do is open up `.gvimrc` and paste in what you got back from the `:set guifont?` command, right? Well, almost right. If there is a space in the font name (like, say “Andale Mono”) you need to escape that space with a slash, like so:

```
1 :set guifont=Andale\ Mono:h14
```

And you’re set. Save the file, source it (`:so %` will still work, but will only do anything if you’re *using* gvim) and you should see your new font in all its glory. This gives you a pattern to follow for any other gui-only settings you want to change. If you want to see a bunch of useful settings see `:h gvim`. There are a lot of *useful* things you can play with, but in the next chapter we’re going to play with a fun one instead.

## 26\. Menus Everywhere! `:h menus`

This isn’t *strictly* a gvim thing, but vim does give you the ability to make your very own menus. They work *better* in gvim than they do in terminal vim, but they *can* work in both places. Be aware, though, that this is a less painless topic than just about anything I have covered in this book.

First off, gvim loads a standard set of menus when you start it. You don’t need to mess with them. You can if you want to; but you’re on your own there. I’m going to cover the basics of creating a brand new menu, and then show you how to make it pop up when you want it, wherever you want it.

There are a lot of caveats in the menu stuff: parts of it work cross platform, parts don’t, so we’re going to cover a basic menu with just a few options. This menu will provide access to Tim Pope’s [fugitive](https://github.com/tpope/vim-fugitive) plugin, letting you run git commands without leaving vim. If you want to follow along *exactly* you’ll need to install that plugin first. Checkout the chapter on [plugins](#chap11.xhtml_plugins) for a quick refresher on how to add stuff using Pathogen.

Okay! Let’s get started. Fugitive gives you access to a plethora of useful git features with parameters and ranges and powerful, intuitive features that we’re going to ignore completely. For now we’re going to provide access to exactly three features:

*   Git Status
*   Git Blame
*   Git Remove

Which, now that we look at it, would make a pretty good layout for our menu!

Fugitive’s `Gstatus` command gives you access to a surprisingly wide array of functions; things like staging or un-staging files, and committing your changes. So naturally it would be the first thing we would want to add to our menu. So hey, I’ll start there.

### Adding a Menu

Adding a menu is similar to adding a keymap: you can set the menu to only work in certain modes, or all modes. You can make it recursive or non-recursive, etc. etc. And, like keymapping, you can test your new menus *before* adding them to your `.gvimrc` file. Let’s test it now: Open a file that is under git control and enter the following:

```
1 :menu Git.Status :Gstatus<CR> 
```

And then hit `<enter>`. You should see a new “Git” menu item appear in your menu bar. If you click it you’ll see a “Status” menu item. Click *that* and you should see the awesome fugitive status screen pop up in a new window. Nice, right? In this example we just used the `:menu` option, which enables your menu in Normal, Visual and Operator-pending mode. There are other options, which leads to a familiar looking table:

Menu Commands

| Command | Modes |
| ——————- | ———— |
| `:menu` | Normal, Insert, Operator-Pending |
| `:nmenu` | Normal |
| `:vmenu` | Visual |
| `:omenu` | Operator-pending |
| `:menu!` | Insert, Command-line |
| `:menu` | Command-line |
| `:amenu` | All |

In this table I kinda saved the best for last there. Most of the time you’ll probably use the `:amenu` option. In fact, there are two shortcuts you can use if you’re just testing menus you haven’t put into your config files yet! The commands `:an` and `:am` are both aliases for `:amenu`^([72](#chap35.xhtml_fn-Typo)).

Okay! Let’s get back to the menu definition we set up earlier. After you choose where you want the menu to be active you name the menu. You’ll notice that we called this one `Git.Status`. The period in the middle defines a *sub* menu, and you can keep going, if you hate your life and want to keep on nesting:

```
1 :menu Git.Should.Be.Easier.To.Use.Than.This.Status :Gstatus<CR>
```

And you get something a little like this:

![Please, please don't do this](images/bad_menu.jpg)

Please, please don’t do this

But now that we’ve had our fun we’re going to go back to *sane* menus, hmm?

### Keeping Things In Order

Unless you’re some kind of crazy bohemian, you’re going to want to define the order in which your menus appear. You do this by adding a *priority* to the menu definition. The lower the priority number, the closer to the left the menu will appear. The default menus have the following priorities^([73](#chap35.xhtml_fn-priorities))

*   File: 10
*   Edit: 20
*   Tools: 40
*   Syntax: 50
*   Buffers: 60
*   Window: 70
*   Help: 9999

In general they suggest *not* setting the priority of your menu higher than 9999, but nobody’s stopping you. To create a menu with a priority you just put the priority before the menu command, like so:

```
1 :80menu Git.Status :Gstatus<CR>
```

Which will put your menu after the Window menu. If you don’t give a priority vim will assign your menu a priority of 500\. If you want to set priorities for sub menus you put the priorities in a dot-seperated list *after* the menu command:

```
1 :menu 80.100 Git.Status :Gstatus<CR>
```

Will put the **Git** menu after window, and set the **Status** menu fairly early on the list (because any menu without a set priority will default to 500).

Okay, so, armed with this information, let’s create the menu for our thee git commands. The following would go well in your `.gvimrc` file:

```
1 :menu 80.1 Git.Status :Gstatus<CR>
2 :menu 80.2 Git.Blame :Gblame<CR>
3 :menu 80.4 Git.Remove :Gremove<CR>
```

Save your file, source it, and you should have a pretty git menu all ready to go.

### Making the Menu Come to *You*

One of the whole points of vim is that you don’t have to move your hands from the keyboard to do things. Which makes menus a problem. You have to pull one hand off of the keyboard, move the mouse *all the way to the top of the screen* to click on some stuff, and then get your hands back into position. Well, we’re going to get rid of one of those steps.

Vim provides a `:popup` command that lets you call a specific menu to the position of your cursor. So, let’s say you want your new git menu. Just go to the command line and type

```
1 :popup Git
```

And the Git menu should show up…somewhere close to your mouse. The behavior of the popup option isn’t *totally* reliable, and it may go away at some point, but for now it looks super awesome. It looks even cooler if you map a shortcut, like so:

```
1 nmap <Leader>g :popup Git<CR>
```

So, armed with this knowledge, we can move on. The problem is that there are two divergent paths from here. Vim on Linux or Windows works pretty much the same, while MacVim has some of its own ideas about life. Choose the section that works best for you.

### Linux and Windows

If you look at the `File` menu on gvim under Linux or Windows you’ll notice that some menu items have underlined letters, and even shortcuts listed to the side of the menu item. You’re probably familiar with these from, well, *every other* program. If you press `<alt>o` when the File menu is open it’ll open a new file. You can define both *accelerator keys* and *reminders* for your menus as well. All it takes is a few little additions to the menu command. Let’s go back to our `Git.Status` entry. If we want to define `<alt>g` as the command to open the Git menu, we would set it up with an ampersand (&) before the letter G:

```
1 :menu 80.1 &Git.&Status :Gstatus<CR>
```

We also set `<alt>s` to be the accelerator key for the status menu item. But let’s say we want to get off of menus altogether. We can have the menu tell us the command we could run if we wanted to avoid the menu. You just put the text you want right-aligned after the literal string `<Tab>`, like so:

```
1 :menu 80.1 &Git.&Status<Tab>:Gstatus :Gstatus<CR>
```

#### Hidden Menus

If you want to be super cool you can set up a menu that won’t appear in the menu bar, a menu that is only accessible as a popup. Again, this is a simple change: the name of your menu needs to have the character `]` at the beginning of its name, like so:

```
1 :menu ]Git.Status<Tab>:Gstatus :Gstatus<CR>
```

And once you’ve defined it this way you need to remember to *call* it with the square bracket:

```
1 nmap <Leader>g :popup ]Git<CR>
```

And viola! You’ve got a menu that appears as if by magic from nowhere! This, my friend, is the good life.

### MacVim is a Special Snowflake!

MacVim handles menus differently, which shouldn’t be surprising, because OSX handles menus differently. If you’re setting up a `.gvimrc` that is expected to be used in MacVim you’ve got two new commands to play with to make your menus fully Mac compatible.

However they’re definitely *not* painless. As in “so far I haven’t been able to add a new menu item using the MacVim menu commands.” You can use the regular menu commands listed before, but assigning mac-specific keyboard shortcuts so far eludes me. And as I already mentioned, you can’t hide menus in MacVim; they’ll always show up on the menubar, even if you preface the name with `]`. So, if you want to learn how to make OSX specific menus check out `:h macvim-menus` from MacVim and let me know what you find.

## 27\. Literary Vim: Writing Prose in Vim

First of all, I have a confession to make: I wrote very little of this book in vim. For the most part I wrote, reviewed, and edited this book in Scrivener, occasionally switching to Multimarkdown Composer for fancy markdown features like tables and such. ^([74](#chap35.xhtml_fn-OtherTools)) This isn’t because vim is a bad choice for prose writing, it more because I have grown quite familiar with and fond of Scrivener over the years, and I find it works well for the way I write prose.

But that’s me. I have had a number of people ask me how to use vim for writing instead of coding. It’s a fair question, and not surprisingly, vim is quite adept at being a writer’s editor of choice. With just a little work you can put the full power of vim behind your blog, thesis, or book about using Scrivener. Turnabout is fair play after all.

### Setting up the a Writing Workflow

When I write prose I almost universally use [Markdown](http://daringfireball.net/projects/markdown/), or, more specifically [MultiMarkdown](http://fletcherpenney.net/multimarkdown/) instead of writing in a word processor like Word, Pages, LibreOffice etc. In this chapter I’m going to go ahead and assume you’re doing the same.

So, to write prose we need a (multi)markdown syntax file, so that vim can help us do all the syntax highlighting and other helpful things it does so well. So far the best I have found is by (you guessed it) Tim Pope, and is available on [GitHub](https://github.com/tpope/vim-markdown). See the chapter on [plugins](#chap11.xhtml_plugins) for a refresher on how to install it.

Later on we’re going to talk about actually *exporting* your markdown-style text to something pretty and fully formatted, so let’s install the software we need for that now, while we’ve already got our hands dirty.

[MultiMarkdown](http://fletcherpenney.net/multimarkdown/) is my converter of choice. It runs on any desktop OS, adeptly converts Markdown and MultiMarkdown into a variety of formats, and is free and frequently updated.

Once you’ve got mmd up and running it’s time to set vim up in writing mode instead of coding mode.

### Writer-Friendly Vim Settings

One of the great benefits of using vim as your main writing tool is that it is one of the original distraction free writing programs. Open vim up full screen and you have nothing to do but write. But there are a few settings we need to tweak to get started.

The first is line wrapping. When you’re programming you usually want each line to stay on its own line, so you can make sure things line up or whatever. When you’re writing prose, not so much. Fortunately, vim has a line-wrapping feature, and it’s easy to use. But you’ll need to make some decisions ahead of time.

The main decision is if you want wrapping on all the time or only occasionally. If you are using vim primarily as a code editor you probably want line wrapping off by default. If you’re using it as a text editor you probably want it on. Since we’re talking about literary vim right now we’ll go with line wrapping on, and then talk about how to toggle it easily.

In order for vim to handle line wrapping intelligently you need to set a few flags in your `.vimrc`:

```
1 set wrap
2 set linebreak
3 set nolist
```

The first one is obvious: we want it to wrap. The second one tells vim to break lines at one of a list of line break characters instead of just saying “okay! That’s 80 columns! Next character goes on the next line!”. It’s the difference between this:

```
1 Here I am on line one. This is a good line. I wo
2 nder when I will hit line two?
```

And this:

```
1 Here I am on line one. This is a good line. I 
2 wonder when I will hit line two?
```

You can check out `:h linebreak” for more information on what characters trigger a line break and how it all works. But for now we’ll just stick with the stock answer: it works very well.

The next thing to say about `wrap` and `linebreak` is that they insert *soft* line breaks instead of *hard* line breaks. A *hard* line break is like actually hitting the `<enter>` key, a *soft* line break only visually moves your text onto the next line. If you make your vim window wider the text will re-flow to the end of the new wider window. If you’re writing in Markdown you absolutely want soft line breaks, as the Markdown parser will format your text appropriately when you run it.

So, what about `nolist`? We turn it off is because `list` breaks wrap and line break. You can read more about it in the help file: `:h list`, but for now let’s just turn it off.

Okay, so now vim is all ready to write! But what if we want to go back to coding? What if we suddenly hate line wrapping? Good question. Let’s add one more line to our `.vimrc` to let us turn line wrapping off anytime we want:

```
1 nnoremap <F7> :set wrap!<CR>
```

The purpose of this command should be fairly obvious. You could map it to something like `<leader>w` if you wanted, but I find that using the `<Fn>` keys for toggling vim behaviors works for me.

### Spreading the Word: How to Get Your Message Out Into the World

At length, it will be time for your words to leave the warm embrace of your computer and fend for themselves out in the real world. It’s a proud and terrifying time. If you’re publishing your opus via some awesome markdown-aware self publishing site like, say, [Leanpub](http://leanpub.com) then your work is pretty much done. Follow their instructions for getting your text on their servers and sit back, a job well done.

However, if you’re using *any other method* of publication we’ve still got some work to do. The reason we wrote in Markdown is because your text can now be converted into whatever format you need, be it PDF, HTML, DOCX, or some other combination of letters. This is where `mmd` comes into play. Let’s take this very simply to begin with. You can practice on the `literary.md` file in the sample files repository.

Okay, let’s say you need to convert your text into an HTML page^([75](#chap35.xhtml_fn-whyhtml)). All we have to do is this:

```
1 mmd literary.md
```

And just like that you’ve got a new HTML page right next to your markdown file. If you pop that page open in a browser you will see that all your text formatting, like tables, italics, bolds, footnotes etc. are there, but precious little other formatting is.

This is because we haven’t told MultiMarkdown what fonts, colors, justifications etc. to use. And while you *could* do that by giving it a stylesheet you want used with your output, I would recommend against doing so. Once you’ve got a basic formatted version of your text you have a couple of options:

*   Turn it over to a publisher and use their formatting
*   Take a pass at your text with a word processor or other program that handles customizable text formatting.

While you were writing it was time to get your words out into the open, get them down in bits so that you wouldn’t forget them. Now it’s time to polish them up, make them look as good as possible for whatever format you choose, and you should really take the time to do that by hand.

### More Formats! I Need More Formats!

The official MultiMarkdown program can convert your text into a list of formats that is impressive, but if you’re like most people you’re going to notice a couple of glaring omissions. Where, for example, is the option to create a `.docx` file for Word, or a PDF file?

The short answer is that mmd can turn your markdown into LaTeX, and you can turn `.tex` files into just about anything, if you want. But that’s probably not the answer you were looking for. Learning the mysteries of LaTeX formatting is probably not what you set out to do. Fortunately there are ways around that.

[Pandoc](http://johnmacfarlane.net/pandoc/installing.html) is one such way. Pandoc seeks to turn just about anything into just about anything else, text-wise. If you wanted to make a Microsoft Word document out of `literary.md` all you would have to do is this: (after installing pandoc, of course)

```
1 pandoc -f markdown_mmd -t docx -o literary.docx literary.md
```

The switches we’re using here are:

*   `-f` incoming format
*   `-t` target format
*   `-o` output file name

And finally the name of the file you want to convert. It’s worth noting that pandoc also doesn’t do PDF output. Microsoft Word, however, does.

But what if you don’t want to write all this stuff on the command line? What if you want live previews of what your text is going to look like, *and* the ability to actually finally create a PDF from your text?

Well, there are apps for that. My favorite app on OSX is [Marked](http://marked2app.com). Marked lets you see how all your formatting is going to look, has a number of built-in stylesheets as well as the ability to add new stylesheets of your own, does a surprisingly wide array of sanity and writing checks on your text, and it can export a PDF of your file. It’s basically a writer’s best friend.

## 28\. Conclusion

Well, here we are at the end of all things Painless and Vimish^([76](#chap35.xhtml_fn-Vimish)). We’ve had some good times, we’ve learned how to do a lot of things in an editor that has been proven (by other people) to be fast and user friendly in the right hands. I hope you’ve seen that you’ve got a great tool at your disposal, and that it isn’t as scary as it looked all those chapters ago when you were first starting out.

But there’s still a long way to go, a lot more to learn. We haven’t covered everything you can do with vim, not by a long chalk. I haven’t even touched topics like writing your own plugins using vim script, and for good reason: I have no idea how to do that. But hopefully at this point you are feeling like those topics aren’t too scary, you’re feeling like you can handle this whole vim thing without fear, and you can hop onto anybody’s computer and use the world’s most built-in text editor instead of making excuses.

Like I said, there’s still a long way to go. Fortunately there is an entire internet full of resources out there to help you reach true vim mastery, if such is your goal. If you just want to *use* vim you’re probably just about there. I’d recommend going back over this material in small bites from time to time as you settle into using vim on a daily basis. Perhaps there was something you read about a while ago that you wanted to try, and now that you’re more comfortable you can add a few new commands to your arsenal. If you want to expand beyond what you’ve read here I’d recommend picking up a more advanced book; there are a few listed in the Appendices. If you want to start writing vim plugins there’s no better time than the present to start learning vim script.

Last of all, I would like to thank you. Writing this book has been an adventure for me. I’ve learned a ton about vim, and about writing, in this process. All the positive comments and suggestions have been deeply felt and appreciated. And your confidence, expressed in the form of actually dipping into your own hard-earned cash and *buying this book* is simply amazing. Again, I thank you.

–*Nate Dickson*

## Appendix 1: Links to References

This appendix is the catch-all for long-form reference discussions that didn’t flow properly in the main text.

### Color Scheme References

(Linked from [Picking a Color Scheme](#chap04.xhtml_picking-color))

*   [Vim Color Scheme Test](https://code.google.com/p/vimcolorschemetest/) has a lot of color schemes listed, with links to the files, and full previews of the scheme rendering different types of files.
*   The [vim-colorschemes](https://github.com/flazz/vim-colorschemes) plugin installs a *ton* of color schemes for you to peruse and sample from the comfort of your own terminal.
*   [Vivify](http://bytefluent.com/vivify/) lets you choose one of *many* color schemes and edit it to your heart’s content.

### Cheat Sheets

*   [Beautiful Vim Cheat Sheet](http://vimcheatsheet.com/): Born on Kickstarter, now out in the wild, this is the cheat sheet that I have pinned up prominently behind my laptop at all times.

### Great Books on vim

*   [Practical Vim](http://pragprog.com/book/dnvim/practical-vim): Presented as a series of tips, *Practical Vim* is a peek into the vim mindset, and a way to make the jump from user to power user. Every time I dip into it I come away with something that extends my vim skills and makes vim just that much more useful for me.
*   [Learning the Vi and Vim Editors](http://amzn.to/16ELAeG) :This is the “everything and the kitchen sink” book on vim. As the title suggests, it also spends a fair amount of time in vi world, and even dives deeper into the underlying `ed` and `ex` editors upon which vim is built. If you want to know it all, this is the book for you.

### Great Sites to Learn more Vim

*   [Vim Adventures](http://vim-adventures.com/): This is a fun site that teaches vim as a video game. You can play a few levels for free, which will help you with the basic motion keys, or pay to get access to the more advanced levels as well.
*   [The Vim Tips Wiki](http://vim.wikia.com/wiki/Vim_Tips_Wiki): What better place to find information about an open source project than a community-maintained wiki? There is a lot of good information on this site for when you’re ready to move beyond the basics and get into some true vim black magic.

### More About Expressions

*   It’s always good to stop in at [Stack Overflow](http://stackoverflow.com/questions/7027741/what-is-the-purpose-of-the-expression-register) for a simple, clear, and concise answer to a question.
*   Andreas Grech has a simple explanation of how to [use the expression register to run ruby files](http://blog.dreasgrech.com/2010/06/extending-vim-with-expression-register.html)
*   *Use Vim* tiptoes into using [VimScript in the Expression Register](http://usevim.com/2013/06/28/expression-syntax/)

### Bundle Managers

In the chapter on [Plugins](#chap11.xhtml_plugins) I covered the Pathogen manager fairly thoroughly, but there are other great options. Here are a couple more that you might want to check out:

*   [Vundle](https://github.com/gmarik/vundle) is a popular plugin manager for vim. You tell it which bundles you want in your `.vimrc` file and it downloads and installs them for you. This is the mirror opposite of how Pathogen works, but it makes it easy to move your entire configuration with you wherever you go.
*   [NeoBundle](https://github.com/Shougo/neobundle.vim) is similar to Vundle in use and in aims, but seeks to improve on some of Vundle’s features.

All of these bundle managers perform more or less the same functions, it’s just a matter of which one works best for you.

## Appendix 2: Quick Reference Charts

### Motions

simple motions

| Keystroke | Motion |
| --- | --- |
| h | move right |
| j | move down |
| k | move up |
| l | move left |
| b | previous word |
| e | end of word |
| ctrl+d | move down by 1/2 screen |
| ctrl+f | move down by 1 screen |
| ctrl+u | move up by 1/2 screen |
| ctrl+b | move up by 1 screen |
| gg | jump to the start of the file |
| G | jump to the end of the file |
| ^ | first non-whitespace character of the line |
| $ | last non-whitespace character of the line |
| `0` | beginning of the line |

### Commands

basic commands

| Keystroke | Command |
| --- | --- |
| d | delete |
| c | change (delete and enter insert mode) |
| y | yank (copy) |
| u | undo |
| p | put (paste) |
| r | replace (with whatever character you press next) |

### Text Objects

Text Object Shortcuts

| Shortcut | Text Object |
| --- | --- |
| w | from the cursor to the end of the word |
| W | from the cursor to the end of the WORD^([77](#chap35.xhtml_fn-wordvsWORD)) |
| s | the current sentence |
| l | from the cursor to the end of the line |
| ’ or “ | a string surrounded in quotes |
| `{` | Everything between two curly braces |
| `[` | Everything between two square brackets |
| `<` | Everything between two angle brackets |
| `t` | Everything inside the closest XML or HTML tags |

### Registers

Named Registers

| Register Keystroke | Name | What Goes In It |
| --- | --- | --- |
| `""` | The Unnamed Register | Every cut or copy |
| `"_` | The Black Hole Register | Anything you want to get rid of |
| `"\` | The Last Pattern Register | A copy of the last thing you searched for |
| `"-` | The Small Delete Register | The last cut or copy that was less than one entire line long |
| `"1` | The Big Delete Register | The last thing you cut or copied that was 1 or more lines long |
| `"2-"9` | Big Delete Register Stack | A running stack of big deletes. `"1` gets pushed to `"2` and so on |
| `"+` | The System Clipboard | If it works. It doesn’t always work |
| `"a-"z` | The Named Registers | Anything you want |
| `"A-"Z` | The Append Registers | Using `"A` will *append* to register `"a` instead of *overwriting* it |

### Folding

Folding Commands

| Command | Option |
| --- | --- |
| `zc` | Close current fold |
| `zo` | Open current fold |
| `za` | Toggle current fold |
| `zC` | Close all possible folds at cursor |
| `zO` | Open all possible folds at cursor |
| `zA` | Toggle all possible folds at cursor |
| `zr` | Reduce folding by one level throughout the document |
| `zm` | Increase folding by one level throughout the document |
| `zR` | Open all folds |
| `zM` | Fold everything |

### Menus

Menu Commands

| Command | Modes |
| —— | —— |
| `:menu` | Normal, Insert, Operator-Pending |
| `:nmenu` | Normal |
| `:vmenu` | Visual |
| `:omenu` | Operator-pending |
| `:menu!` | Insert, Command-line |
| `:menu` | Command-line |
| `:amenu` | All |

### Tab Commands

*   Opening a new tab:
    *   `:tabnew` *filename*
    *   `:tabe` *filename*
*   Close current tab
    *   `:tabc`
        *   `:tabclose`
        *   Note that both of the above methods can take a `!` to force the tab to close even if there are unsaved changes in a buffer.
*   Close other tabs
    *   `:tabo` Close all other tabs.
*   Go to the next tab - `gt` - `:tabn`
*   Go to the previous tab - `gT` - `:tabp`
*   Go to a specific tab - `:tabfir` goes to the **first** tab - `:tabl` goes to the **last** tab - *tabNumber*`gt` Goes to the tab number given - *tabNumber*`gT` Goes to the tab number given
*   Reorder tabs - `:tabm`*number* places a tab **after** the given tab number. Use 0 to make the current tab first. - `:tabm +`*number* move a tab *number* places **right** - `:tabm -`*number* move the tab *number* places **left**
*   List all open tabs - `:tabs`

## Appendix 3: Sample `.vimrc` files

This section gives you a look at a couple of simple (but functional) `.vimrc` files, with annotations. Note that these aren’t *my* `.vimrc` file, although they are more or less *based* on mine. These are intended to be simple starting points from which you can get ideas. You could use these for a while, tweak them, and get to where you’ve got something you’re happy with over time.

If you want to see what I’m using right now you can view it on [GitHub](https://github.com/PogiNate/dots/blob/master/home/.vimrc). I try to back it up regularly. You could theoretically copy mine directly, but it’s got a lot of things in it that you don’t need, unless you’re one of the five other people on Earth who do XQquery development for a living.

For that matter, if you’re not keeping your `.vimrc` and other files backed up on an online service, now would be a good time to start. There are few things more frustrating than realizing all your customizations have just disappeared without a trace.

Okay, without further ado, the absolute simplest, most basic sample file that I would actually use:

* * *

```
 1 "This tells vim to only run as VIM, not as vi"
 2 set nocompatible		
 3 "Remember that it has to be in your ~/.vim/colors folder"
 4 colorscheme jellybeans 	
 5 "Displays line numbers down the left side of the screen"
 6 set nu				
 7 "Change the <leader> key to comma instead of \ "
 8 let mapleader=","		
 9 "enable syntax highlighting"
10 syntax on				
11 "Handle things like indents and plugins intelligently." 
12 filetype plugin indent on	
13 
14 "Make the Backspace Sane"
15 "The Backspace in vim is weird by default."
16 "This makes it behave the way you expect."
17 set backspace=2
18 "More backspace sanity"
19 set backspace=indent,eol,start 
20 
21 " Pathogen settings"
22 " This line tells vim to load all your Pathogen-installed plugins."
23 " Naturally, Pathogen needs to be installed before this works."
24 execute pathogen#infect() 
```

A sample .vimrc file

```
 1 " This tells vim to only run as VIM, not as vi"
 2 set nocompatible
 3 
 4 " Any color scheme in your ~/.vim/colors folder"
 5 colorscheme jellybeans 	
 6 
 7 " Displays line numbers down the left side of the screen."
 8 set nu				
 9 
10 "Change the <leader> key to comma instead of \ "
11 let mapleader=","		
12 
13 "Turn tabs into spaces when saving."
14 "I prefer this, as it keeps things orderly."
15 set expandtab    		          
16 
17 " Wrap long lines."
18 set wrap                                    
19 
20 " Enable syntax highlighting"
21 syntax on				
22 
23 "Handle things like indents and plugins intelligently."
24 filetype plugin indent on	 
25 
26 "Make the Backspace Sane"
27 set backspace=2		 	
28 set backspace=indent,eol,start
29 
30 " Pathogen settings"
31 " Use pathogen with it's pun-filled method names."
32 execute pathogen#infect()	
33 
34 "Folding"
35 " You can set this to 'indent' or 'syntax' if you like;" 
36 " I prefer manual"
37 set foldmethod=manual 
38 " This tells vim to only fold one level at a time."
39 set foldlevel=1 
```

A slightly longer .vimrc file

## About This Book

### About the Text

*Painless Vim* is by Nathanial Ellsworth Dickson, but you can call me Nate.

It was written using an unwieldy combination of (in alphabetical order):

*   [Marked](http://markedapp.com/)
*   [MultiMarkdown Composer](http://multimarkdown.com/)
*   [Scapple](http://www.literatureandlatte.com/scapple.php)
*   [Scrivener](http://www.literatureandlatte.com/scrivener.php)
*   [Ulysses](http://www.ulyssesapp.com/)
*   [vim](http://www.vim.org/) (of course)

It was written on an unlikely number of macs.

### About the cover

The cover features an illustration by [Callihan](http://www.shutterstock.com/pic.mhtml?id=94462300). Used with permission. The typefaces used on the cover are:

*   **Matchbook Serif** (*title*)
*   **Aleo Light** (*subtitle*)
*   **Caviar Dreams** (*by line*)

The cover was designed by Nate Dickson using [iDraw](http://www.indeeo.com/idraw/) and [Pixelmator](http://www.pixelmator.com/)

## Special Thanks

I would like to thank, first and foremost, my dear Libbie, for her support, kind words, encouragement, proofreading, spell checking, questions, and love. I’m the luckiest husband ever.

Slightly less mushy thanks also go out to my team of underpaid (indeed *un*paid) proof readers:

*   Holly McNeil
*   Jesse Booth
*   Joanna Noall
*   Josh English

## Notes

1You and I aren’t the only ones that feel this way. Even [very smart people](http://yehudakatz.com/2010/07/29/everyone-who-tried-to-convince-me-to-use-vim-was-wrong/) can get caught by the “throw the newbie in the deep end” problem.[↩︎](#chap00.xhtml_fnref-Katz)

2A few months ago[↩︎](#chap01.xhtml_fnref-1)

3According to me, see the whole “Opinionated” thing up above.[↩︎](#chap01.xhtml_fnref-2)

4[http://natedickson.com](http://natedickson.com)[↩︎](#chap01.xhtml_fnref-3)

5[http://crazyapplenews.com](http://crazyapplenews.com)[↩︎](#chap01.xhtml_fnref-4)

6[@poginate](https://twitter.com/poginate)[↩︎](#chap01.xhtml_fnref-6)

7[http://github.com/PogiNate](http://github.com/PogiNate)[↩︎](#chap01.xhtml_fnref-7)

8I’m going to use lowest common denominator words like “Terminal” a lot. If your OS calls it something different like a shell or a command line or (heaven help you) `cmd.exe` then just substitute that in your head.[↩︎](#chap02.xhtml_fnref-term)

9Later on you’ll want to know that this is the “quit and don’t save anything” way of getting out. There are a few other ways to exit vim, but we’ll get there later.[↩︎](#chap02.xhtml_fnref-out)

10Remember that commands that start with a colon `:` require you to press `<enter>` to make them execute. Okay, this is definitely the *last* time I’m going to repeat that. [↩︎](#chap03.xhtml_fnref-lastWarning)

11I’ve heard it said that some people call Normal Mode “Beep Mode” because you’ll try to switch back to it and the terminal will beep at you and you’ll realize you’re already in it. I don’t know if I believe that anybody actually calls it that, but since I’m writing a vim book I’m honor bound to pass this bit of information on to you. Just like if I were writing *Beginner’s Big Book o’ Computer Facts* I would feel obligated to mention that four bits is called a “nibble” (because it’s *half a byte* and “byte” sounds like “bite”! Get it? *GET IT???*), even though I’m pretty sure that’s just a joke that got put in some textbook years ago and has since gotten out of hand.[↩︎](#chap03.xhtml_fnref-Beep)

12“There is more than one way to do it” usually pronounced “Tim-Toady”[↩︎](#chap03.xhtml_fnref-timtowtdi)

13Here are two secret bonus ways to exit vim that you won’t need to know about until you know how to open multiple files: `:qa` closes all open files and quits vim, and `:qa!` does the same thing even if any file has unsaved changes. Don’t worry, we’ll review them again when we talk about [opening multiple files](#chap22.xhtml_tab-pages).[↩︎](#chap03.xhtml_fnref-SecretBonus)

14On windows the situation is a [little more complicated](http://superuser.com/questions/86246/where-should-the-vimrc-file-be-located-on-windows-7). We’re going to proceed as if you’re on a Unix-ish machine, because it’s easier. [↩︎](#chap04.xhtml_fnref-WinVim)

15Or people who write vim books in Markdown. [↩︎](#chap04.xhtml_fnref-OrMarkdownUsers)

16which is unix-speak for “[read a file and do what it says](http://stackoverflow.com/questions/9326695/what-does-it-mean-to-source-a-file-in-unix-linux-context)”[↩︎](#chap04.xhtml_fnref-read)

17And it actually cost me some cash money, but not a ton.[↩︎](#chap05.xhtml_fnref-money)

18Until I created my own, that is.[↩︎](#chap05.xhtml_fnref-Until)

19By programmers at any rate. Managers would suggest that at least a portion of that 90% is *actually* spent furtively reading tech blogs and web comics.[↩︎](#chap06.xhtml_fnref-programmers)

20I use the name “motions” instead of “commands” or “actions” quite intentionally. For now don’t worry about it, just remember it for later.[↩︎](#chap06.xhtml_fnref-motions)

21I’m only going to cover this once, because it’s annoying. Fans of vi will insist that you pronounce “vi” like “vee eye” instead of like “vie” because shut up. “vim”, thankfully, is pronounced “vim”. This is yet another reason to never ever use non-improved vi.[↩︎](#chap07.xhtml_fnref-veeeye)

22Once on the first word of the sentence, once on “Larry” and once on “Wall”.[↩︎](#chap07.xhtml_fnref-threeTildes)

23to make “fred” “dead”.[↩︎](#chap07.xhtml_fnref-roperator)

24We’ll get to things like changing words and sentences soon enough. Don’t worry, I won’t leave you hanging.[↩︎](#chap07.xhtml_fnref-words)

25Like, say, a book about how vim works.[↩︎](#chap07.xhtml_fnref-longform)

26If you know it. Or you can just type three periods (which you can call an ellipsis, if you know that) and call it good.[↩︎](#chap07.xhtml_fnref-IfYouKnow)

27You would think that I would repeat myself here, wouldn’t you? I know. I’m just as surprised as you are.[↩︎](#chap07.xhtml_fnref-Repeating_myself)

28Wondering what that `w` means? Good eye. We will be getting to that right after the aside. [↩︎](#chap08.xhtml_fnref-shortly)

29I’ll get to the difference between a lower case word and an upper case WORD very soon. [↩︎](#chap08.xhtml_fnref-wordvsWORD)

30There is a lot of discussion about what this is actually called. I’ll let you dive into that fun world of terminology on your own some other time. I believe my nomenclature for things like *motions, counts, operators* and *commands* makes sense, and won’t get you lost when you start diving into vim’s [help system](#chap17.xhtml_help).[↩︎](#chap08.xhtml_fnref-count_terminology)

31Or possibly five words and a protocol specification.[↩︎](#chap09.xhtml_fnref-not-counting)

32Contemplation of your navel as an aid to meditation. [Really.](http://en.wikipedia.org/wiki/Omphaloskepsis)[↩︎](#chap09.xhtml_fnref-omph-def)

33Sorry about the super-technical jargon there.[↩︎](#chap10.xhtml_fnref-letter-command)

34For that matter, writing *prose* isn’t usually a linear process anywhere other than junior high either. But we’ll stick with the metaphor for now. It’s probably worth pointing out that I don’t know anything about art, so the following analogy may be a bit odd.[↩︎](#chap10.xhtml_fnref-write-draw)

35See what I did there?[↩︎](#chap10.xhtml_fnref-seethere)

36Technically they both move the cursor by one `shiftwidth`, which is *usually* four spaces and is *usually* the same as one tab.[↩︎](#chap10.xhtml_fnref-indentoutdent)

37technically a page from vim’s official help system, which we will get to [soon](#chap17.xhtml_help).[↩︎](#chap10.xhtml_fnref-vim-help-modes)

38I’m just kidding. Kind of. You could also be adding a comma to the end of every line in an array or list of attributes.[↩︎](#chap12.xhtml_fnref-Kidding)

39With the odd exception of `O` to open a new line above your current line. [↩︎](#chap13.xhtml_fnref-noO)

40but disabled by default[↩︎](#chap13.xhtml_fnref-disabled)

41From this point on I’m going to omit the double quotes before register names, because they look *really weird* in text. Just remember that if I write “register b” that what you should enter in vim is `"b`. [↩︎](#chap14.xhtml_fnref-regnames)

42Unless you name a register. Then it gets stored *three* places.[↩︎](#chap14.xhtml_fnref-ThreeReg)

43they’re stored, along with quite a few other things, in a file called `.viminfo`. But that’s a topic for a different book. [↩︎](#chap14.xhtml_fnref-Viminfo)

44It’s not really *really* gone, of course. if you just hit `u` it’ll spring back to life. It’s really hard to get rid of things in vim.[↩︎](#chap14.xhtml_fnref-notforever)

45I am using one called [Jellybeans](https://github.com/nanotech/jellybeans.vim). Because it’s awesome, that’s why.[↩︎](#chap15.xhtml_fnref-current-theme)

46The “c” stands for “close”. I’m not sure why “z” stands for “fold”.[↩︎](#chap15.xhtml_fnref-cIsClose)

47This is not because I’m a terrible writer. I hope.[↩︎](#chap16.xhtml_fnref-badwriter)

48Because you are good at regular expressions and feeling pretty good at vim as well right now.[↩︎](#chap16.xhtml_fnref-good_at_regex)

49Generally called `PCRE` or “Perl Compatible Regular Expression” parsers.[↩︎](#chap16.xhtml_fnref-pcre-parsers)

50This should remind you that `:q` isn’t `quit` the way you would normally think of that verb. In fact, this is (yet another) good reason to use `ZZ` instead of `:qs` and `ZQ` instead of `:q!`; it breaks the mental link between the command and the thought of “quitting” vim. [↩︎](#chap17.xhtml_fnref-q_is_not_quit)

51It shouldn’t surprise you because I told you that at the beginning of the chapter.[↩︎](#chap17.xhtml_fnref-nosurprise)

52I’m saying `ctrl+s` here, knowing full well that my mac using brethren are all saying “it’s COMMAND s, thank you so much.” Relax friend. I’m writing this on a MacBook Pro, I agree with you. But we’re still a minority, so just..just be cool, okay?[↩︎](#chap18.xhtml_fnref-ctrl_cmd)

53Not mine; Bram Moolenar (the guy who created vim) coined that phrase as a way to understand the vim way. Most people who work with text on a regular basis can touch type: they can find all the letters without looking as long as their index fingers can find the small marks on j and f. Touch editing means that you can do *all* the things you would do when you’re editing a program by just finding those two keys and never looking at the keyboard. [↩︎](#chap18.xhtml_fnref-touch-edit)

54Hog Bay Software’s [Quick Cursor](http://www.hogbaysoftware.com/products/quickcursor) makes it very quick and easy to jump from any of the above editors into vim and back, so that I have the touch-editing power of vim in addition to whatever feature I was using in the other editor.[↩︎](#chap18.xhtml_fnref-Quickcursor)

55With great power comes great responsibility.[↩︎](#chap19.xhtml_fnref-spiderMan)

56But *seriously* don’t do that. It’s just an example. [↩︎](#chap19.xhtml_fnref-butdont)

57It’s worth noting that you can map the Alt key in a similar way: the pattern is <M-`n`>, where `n` is whatever letter you want to press along with the alt key. However, we’re going to stick with vim tradition and avoid the alt key as much as possible, lest people think we are emacs users.[↩︎](#chap19.xhtml_fnref-mappingAlt)

58Some of you may have noticed that it’s as quick or quicker to just *type* `ea` as it is to type `,e`. That’s part of why I told you not to map this one.[↩︎](#chap19.xhtml_fnref-justasquick)

59I don’t have wallpaper either, but you’re probably familiar with the image: you push down a bubble in one place and it pops up somewhere else. Also, in general, wallpaper is *really ugly*. [↩︎](#chap19.xhtml_fnref-wallpaper)

60I’ve rewritten this sentence approximately thirty times and can’t think of a better way to say that.[↩︎](#chap19.xhtml_fnref-rewrites)

61Normally four spaces. But you can change it by adding a line like `set shiftwidth=2` to your `.vimrc` file.[↩︎](#chap20.xhtml_fnref-shiftwidth)

62Yes, technically it’s a *buffer*, not a real *file*, but we’re going to gloss right over that point.[↩︎](#chap21.xhtml_fnref-file-buffer-redux)

63*rimshot* Thank you, thank you, I’ll be here all week.[↩︎](#chap21.xhtml_fnref-rimshot)

64I give. It’s more or less a mode, and it’s easier to talk about as a mode.[↩︎](#chap21.xhtml_fnref-wcm)

65A book entitled *Painless Tmux*, perhaps? I wonder if that will ever be a thing? (This is a thing we authors call *forshadowing!*)[↩︎](#chap22.xhtml_fnref-another_book)

66Contrast that with Google Chrome, which is about 5 years old and is on version 30.[↩︎](#chap24.xhtml_fnref-chrome)

67Technically one `shiftwidth`, but who’s counting?[↩︎](#chap25.xhtml_fnref-shift-width)

68I know that’s not really a word, but it’s easier to say than “reduces the indentation level” the entire region by one tab.[↩︎](#chap25.xhtml_fnref-outdent)

69Remember, in unix land when we say something “sources” a file we mean it “reads that file and does what it says.”[↩︎](#chap26.xhtml_fnref-reads)

70And take up your entire day as you find new settings you want to add to your `.vimrc`[↩︎](#chap26.xhtml_fnref-allday)

71Technically they were added to a struct that mapped an integer to a standard color name, but you only care about that if you’re a C developer who wants to create a new shell that implements the ANSI colors.[↩︎](#chap26.xhtml_fnref-colornames)

72I’m not sure why `:an` is in there. I like to believe that someone just kept hitting the wrong key and finally decided to map the command so that it would work.[↩︎](#chap27.xhtml_fnref-Typo)

73you can see this list in the help text by using `:h menu-priority`[↩︎](#chap27.xhtml_fnref-priorities)

74See the [About](#chap33.xhtml_About) section for more information on other tools used in the creation of this book.[↩︎](#chap28.xhtml_fnref-OtherTools)

75We’re converting it to HTML first for two reasons: 1.) it’s the easiest and 2.) because you’ll quickly see just how *not* ready for primetime the output is. [↩︎](#chap28.xhtml_fnref-whyhtml)

76No, it probably isn’t a word, but I’m sticking with it.[↩︎](#chap29.xhtml_fnref-Vimish)

77I’ll get to the difference between a lower case word and an upper case WORD very soon. [↩︎](#chap08.xhtml_fnref-wordvsWORD)