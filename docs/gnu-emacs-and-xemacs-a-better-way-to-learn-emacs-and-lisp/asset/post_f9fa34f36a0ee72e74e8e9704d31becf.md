
# PART I
# How Emacs Evolves to Suit Your Needs

- 1 How Emacs Differs from Other Software
- 2 Acquiring and Installing Emacs
- 3 Overview of Basic Emacs Skills
- 4 Using the Built-in Customization Tools
- 5 Emacs-Lisp As an Entry Point to Configuration
- 6 Learning the Vocabulary of Emacs-Lisp
- 7 A Sample Emacs-Lisp File
- 8 Byte-Compiling for Efficiency

![](img/c8827ea52a0796def3f6891892ed9d3a_38_0.png)

# Chapter 1: How Emacs Differs from Other Software

- Software and the User
- Emacs Vocabulary and Conventions
- Key Conventions
- Emacs and Emacs-Lisp
- How Emacs Evolves to Suit Your Needs

What sets Emacs apart from other editors is the extent to which the “guts” of the program are exposed to the user. You don’t have to know much Emacs-Lisp to take advantage of this trait. Throughout this book, techniques to help you delve into the inner workings of Emacs will be illustrated at whatever level you are comfortable with.

Your work with Emacs, whether motivated by curiosity or by the need to change the editor to suit your needs, can be quite a bit of fun. It tends to be an episodic activity, with bursts of customization (perhaps sparked by a Usenet posting or the release of a new package) followed by periods of just using the editor. Slowly but surely, as time passes, a new, personalized Emacs emerges. This book should speed up the process.

## Software and the User

Emacs is a perfect example of the principles underlying the GNU project. The editor, including the source code, is free—with a few important qualifications. Emacs is released under the GNU General Public License. This license allows you to freely share the software but specifically forbids changing the software and releasing it as a proprietary application. This ensures that development will remain open and that the application remains free. In effect, the license prevents anyone from making money by selling a closed-source binary version.

### Free Beer and Free Speech

The word “free” has several shades of meaning; this often leads to some confusion as to what the word really means when applied to software licensed under the GPL. Though this software can be obtained free of charge, another sense of the word “free” is more significant. The eighteenth century philosopher Thomas Locke defined this sense well:

> “Exempt from subjection to the will of others; not under restraint, control, or compulsion; able to follow one’s own impulses, desires, or inclinations; determining one’s own course of action; not dependent; at liberty.”

A comparison often encountered in GNU documentation contrasts free beer and free speech. Free beer doesn’t come with the recipe!

### Commercial Versus Open-Source

Although there is a thriving market for commercial software, there is also a downside for the users. Most people have had the experience of investing money in a proprietary software application and spending time learning to use it effectively, only to see the company that developed and marketed the application either discontinue further development or go bankrupt. Once this happens, the software is *orphaned*, and as hardware and operating systems evolve, chances are good that the application will quit functioning at some point.

Another problem from the user’s point of view is proprietary binary file formats. A file saved in such a format typically can be read only by the application that generated it. If the application is orphaned and quits working, the user risks losing valuable personal files.

> If a commercial software firm decides that there is no more money to be made selling one of its products, the company might quit updating it (fixing bugs and so on) and let it languish. The normal tendency is to keep the underlying source code private to prevent competitors from benefiting from their work. This software has been *orphaned*.

![](img/c8827ea52a0796def3f6891892ed9d3a_42_0.png)

When you buy a piece of commercial software, chances are that in a year or two you will be encouraged to upgrade to a new version. On the face of it, this seems to be a good thing: the company is working hard to improve its software, and you as the user/customer will benefit from bug fixes and new features. This is often the case, but on the negative side, companies sometimes change their saved-file format in such a way that a user of the old version is unable to exchange files with other users who have upgraded. What if the old version works fine for you and you have no need of the new features in the new version? Not every software firm is guilty of this “forced upgrade” practice, but it does happen.

Open-source software developers tend toward “universal” file formats—those that are written in ASCII text and can be read by other applications. Of course, many types of software that people need simply are not available in a freely licensed version. Members of the open-source community have two different approaches to this situation. The purist approach is to wean yourself from needing proprietary software, making every possible effort to find ways to accomplish your work using only open-source tools. The more moderate approach is to use free software when it suits your needs and to use commercial software when there is no open-source equivalent.

Naturally, open-source software projects sometimes lose momentum and go through static periods. Perhaps another, more useful software project has drawn away users or developers, or the maintainers have lost interest. What really matters is that the source is still available. If the software still serves anyone’s needs, eventually a developer will happen across it and either take it on as a personal project or use parts of the code in a new piece of software. The work that the original developers released to the world is never completely lost; rather than reinvent the wheel, it is likely that the old code will be adapted or reused.

Writing software can be pure drudgery when done for purely monetary reasons, as any work can be. It can also be enjoyable and challenging when the results are useful to the developer and to other people using the software. There has been much speculation as to the motives which cause developers to write free software. The consensus seems to be that a personal mix of the following motives are largely responsible:

- The urge to “scratch an itch,” or to solve a particular problem.
- The pleasure that accompanies any creative activity.
- Peer approval of the resulting software.
- Altruism; sometimes a little greed will help many people.

Companies can also benefit from having the source to some software available. Outside developers may add features that they need and contribute them back to the company. Knowledgeable users may contribute bug reports as well.

## Methods of Customization

Nobody likes software that confines the user in a straitjacket of unchangeable default settings. Most applications cater to people’s natural desire for customization by allowing settings to be changed and saved in some sort of configuration file that is read whenever the application starts up. The most common approach is to have a configuration dialog box, a window that can be summoned from the menu bar and that contains a series of options. These dialog boxes can be quite extensive, but the problem with them is that each configuration option has to be compiled into the application. Expensive development time must be devoted to first figuring out what a user might want to change and then writing the code to allow that option to appear in the configuration dialog box. There is a fair chance that a default setting that you would really like to change wasn’t included.
