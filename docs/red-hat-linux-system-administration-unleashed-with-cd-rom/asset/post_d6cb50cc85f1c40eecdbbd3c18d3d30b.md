
There are two strategies that you can use when dealing with these users, the first being to respond to them with the same type of answer. When this type of user makes a request of you that could be dealt with by the user after a short training session, he will invariably tell you that he does not have the time to spend learning what you have to teach. One response in this case is to outline the projects on which you are working that will suffer if you have to do his work for him. Ask him which of the projects he is willing to take responsibility for when it slips. When the user starts to realize that you are going to use his lack of cooperation as an excuse for missing deadlines, he sometimes comes around to your way of can be very effective with people who are power users. They almost always have the skills required to help themselves, but are reluctant to do so for any number of reasons. For this strategy to have the most impact, you should in your response to the request outline the steps you took to resolve the issue and be sure to send this information to the user and to the user's manager. This is important because it lets the manager know the level of effort required to resolve the issue so that if the user attempts to blame you for slowing down his work, the manager will know how easily the user could have solved the problem for himself.

## The “I Can Do That Myself” User

At the opposite end of the spectrum from the user unwilling to take time to learn new skills is the user who wants to do everything himself. This is the type of user who will ask for administrator privileges on his desktop system, then come complain to you when it breaks. These users are often the ones who have enough knowledge to be a security risk on your network and bear the most watching.

The immediate response to requests for root authorities on the desktop should almost always be no. In the large network environment, consistency is the key to a manageable network. If each user is permitted to alter his system as he sees fit, it makes the task of system maintenance nearly impossible. To guard against this type of user, it is often necessary to employ measures like Tripwire or other systems for checking the consistency of systems.

In the small company environment, another key to keeping these users in check is to massage their egos by asking for their assistance in project planning or in user training. By showing them that you respect their abilities, you can get them to assist you in ways that are not threatening to your network. If they feel that you respect their opinions and will listen to their concerns, they are more likely to bend to your policies than if you try to be a hard liner with them.

The thing not to do with this type of user is to give him limited power. The power user will chafe at the restrictions you place on him, but will usually learn to live within your boundaries if all users are given the same capabilities for dealing with their systems. Once you give them privileges outside that of the normal user, they will almost always seek more, often enlisting the aid of their managers to pressure you into giving them even more control over their systems. Once this trend gets started, it is next to impossible to stop.

## The “I Just Have a Quick Question” User

This type of user is one of the most troublesome to deal with because he comes to you out of genuine curiosity. The problem with these users is that many times the question and the answer are not required to accomplish their job, but is something that they stumbled across in the course of the day. They tend to initiate interruptions with phrases like, “If you are busy, I can come back later,” or “I just have a quick question.” You are drawn in by their lack of aggressiveness and because they were courteous enough to ask if you were busy, you tend to want to try to help them immediately. The problem with these users is that once you have answered their quick question, you realize that you have opened the door on a related subject that will take much longer to explain.

My response to these users is to try to redirect their queries to sources of information other than myself. For example, if a user is interested in what new features have been added to the latest Linux kernel, I would direct him to a Web site like Kernelnotes.Org, where he can find the information he is looking for without requiring my time.

These are just a few of the problem user types, and how you deal with them is largely dependent on how your company is organized. The key to dealing with all users is to provide a structure for interaction with them and to live by that defined structure.

## Grant No Exceptions

There is an old saying that states that the exceptions prove the rule; however, in dealing with users, exceptions destroy the rules. This is true for several reasons, the most common being what I like to call the kindergarten lament, or "He has one, why can’t I?" No matter how professional your user group is as individuals, as a whole, they will more often than not act like a group of spoiled children. This is why any allowed deviations from policy must be outlined as an addendum to that policy.

Take, for example, the assignment of email aliases for users. I have often seen a policy established in a company that all user names will adhere to either a first initial, last name or a first name, last initial standard. This can often lead to confusing login names that are hard to remember and when this policy is enforced, it will often generate requests for email aliases that are easier to remember. This may sound innocent enough, but consider how to deal with requests for first names as aliases. It might work if no one shared the same first name, but consider how many Mikes or Toms or Bills you are likely to have in a company of 150 people. Who gets the alias bill? What do you do if you gave the alias bill to the company mail clerk and then you hire a CEO with the same first name? As you can guess this could quickly evolve into a big problem. The solution is to make a policy that prohibits single name aliases and to grant no exceptions.

## Summary

This chapter attempted to outline some of the issues that arise in dealing with the users of your systems. It talked about ways to deal with problem users and some of the ways to handle the inevitable interruptions that users generate. It looked at how a help desk can help to manage these problems, what features a help desk should be capable of supporting, and some manning strategies for your help desk. It also gave you a pointer to a tool available for Red Hat Linux to help you set up a help desk. Finally, it covered the importance of establishing policy and sticking to it. Take this information as what it was intended to be—advice—and develop your own strategies for dealing with the users of the systems you administer.

## Shells, Scripting, and Automation

## PART IX

## In This Part

- 31 Shells 925
- 32 Shell Scripting 967
- 33 Automation 1017

## Shells

## In This Chapter

- Getting Started with Shells 926
- bash, the Bourne Again Shell 928
- tcsh, the Enhanced C Shell 945
- Other Shells 964

This chapter looks at using Linux command-line interpreters, known as shells. It covers the two most popular shells, bash and tcsh, in detail; it also touches quickly upon some of the other shells that are available.

## Getting Started with Shells

The task of administering a Red Hat Linux system involves being able to communicate with that system. Although many graphical tools are available to do this job, the true power of the administrator is only available through a shell. A shell is a program that allows you to communicate with the operating system through a series of commands. The original shell developed for the first version of UNIX was known as the Bourne shell; today the Bourne lives on in the form of bash, the Bourne Again Shell. Many different shells have been developed over the years, each having its own unique features while at the same time adhering to basic standards that allow users to move easily from one shell to another. Red Hat Linux 6.0 comes with several different shells, including ash, bash, pdksh, sash, tcsh, and zsh. Those names may look a little daunting at first glance, but don't let that fool you. Once you master one shell, you can pick up any other shell almost immediately. The default shell installed on Red Hat Linux, and also the default shell on most other Linux distributions for that matter, is called bash.

If you boot into a text mode login, you start your default shell simply by logging in. However, if your system boots directly into the X Window System (via GDM) you will have to open an xterm to start your default shell. Once you have started your shell you can find out what shell you are running by printing out the contents of the SHELL environment variable. You can use the following command to do so:

```
$ echo $SHELL
```

Unless you have modified your default shell, this command should output /bin/bash.

## Differences Between the Shells

If you decide to try out some different shells during your usage of Linux, you will find that most of the shells act the same for almost all the basic commands. The main differences between the shells become apparent when you start trying out some of the more advanced features, and especially when you start trying out some shell programming. Most shells descend from either a Bourne-shell programming syntax or from a C-shell programming syntax, and there are some crucial differences. Programs written to run under the Bourne shell will probably not work under the C shell, and vice versa. It pays to learn both styles of shell programming; however, the Bourne-shell style is much more common than the C-shell syntax and many also consider it easier to learn.
