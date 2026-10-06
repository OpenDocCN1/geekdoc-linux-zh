# What Is a Shell?

As you noticed, I mentioned the results of the finger command showed I was using the Bash shell, so you may well be wondering what Bash is. Well, Bash (Bourne Again Shell) is one of the many shells that are used in Linux systems, and it is the one that happens to be with your Ubuntu distro (and most others, for matter). A shell is a program that interprets the commands you type into the Terminal and delivers them, so to speak, to your system that it can act upon. I like to think of it as a command-handling sub-system, for which the Terminal acts as a graphical frontend.

# What Is a Plan?

I also mentioned that the results said I had no plan, so you may also be wondering what it is all about. A plan is a small file kept in your folder that other users see when they use the finger command out. Traditionally, a plan file contained information about where you were going to be or what you were working on. These days, however, most people use them to leave odd little messages, quotations, or whatever, as they do in their signatures. Take a look at Figure 8-9 to see what happens after I add a .plan to my folder.

```
rgmydesktop:~# finger rg
grmydesktop:~$ finger rg
Login: Name: Rickford Grant
Directory: /home/rg
Shell: /bin/bash
Since Wed Mar 21 15:33 (EDT) on pts/1 from :0
No mail.
Plan:
I was the victim of a series of accidents. . . as we all.\ngrmydesktop:~$
```

Figure 8-9: Output from the finger command with a plan

You can now see my plan, which is a quotation from Kurt Vonnegut's The Sirens of Titan (or Al Stewart's story by the same name, for that matter). Of course, you can put anything you want in yours. You will get the chance to create your own plan file in "Project 8A: Creating a Plan" on page 141, if this seems fun to you, more is in store.

# Other Uses of the Finger Command

Before moving, I should mention that you can also use the finger command to do a little domestic espionage of sorts. Let's say your friend, Chris, has a user account on your machine. Chris, who wants your permission to go to the movies, claims have been hard at on the computer all day writing a report for school. Having your doubts, you could type finger chris to see what the facts actually are. It may be a bit underhanded and rotten, but it