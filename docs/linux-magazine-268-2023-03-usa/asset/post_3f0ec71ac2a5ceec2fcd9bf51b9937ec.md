
# GET TO KNOW ADMIN

![](img/e3f454b04d121b3b3750fddfda8dd21e_30_0.png)

*ADMIN* Network & Security magazine is your source for technical solutions to real-world problems.

ADMIN is packed with detailed discussions aimed at the professional reader on contemporary topics including security, cloud computing, DevOps, HPC, containers, networking, and more.

**Subscribe to ADMIN** and get 6 issues delivered every year.

Want to get ADMIN in your inbox?

**Subscribe free to ADMIN Update** and get news and technical articles you won't see in the magazine.

bit.ly/HPC-ADMIN-Update

![](img/e3f454b04d121b3b3750fddfda8dd21e_30_1.png)

ADMIN Network & Security

- @adminmagazine
- @adminmag
- ADMIN magazine
- @adminmagazine

# Enhanced searches with fzf

**Fuzzy Finder**

Simplify your searches and get better results with fzf, a modern search tool based on fuzzy logic. By Bruce Byfield

S**earch commands have always been essential to using computers. With the increased storage capacity of modern systems, they are more important than ever because there is more material to search. In fact, searches are so important that alternatives to time-honored commands are becoming increasingly common. One of the most effective of these recent alternatives is *fzf*, a command-line “fuzzy finder” [1].

For most Linux users, the basic search tool for finding directories and files has been *find*, which is most effective when you know exactly what you are looking for. If you do not know, then you need a way to allow variation in the output.

- **Author**
  Bruce Byfield is a computer journalist and a freelance writer and editor specializing in free and open source software. In addition to his writing projects, he also teaches live and e-learning courses. In his spare time, Bruce writes about Northwest Coast art (http://brucebyfield.wordpress.com). He is also co-founder of Prentice Pieces, a blog about writing and fantasy at https://prenticepieces.com/.

Traditionally, variation in search tools like *find* is provided by regular expressions (regexes), a concept first developed in the 1950s. Regexes are standard patterns that offer different types of variations in results. Most users are familiar with the simpler regexes, such as \* to mean zero or any character, so that apt\* might return apt, apt-get, apt-cache, and probably many others. At a more advanced level, users might know that grep|grey produces results with either spelling, or [b-e] a range of characters. However, regexes are not consistent across applications and can rapidly become extremely complex to construct or type correctly, especially when all you want is a quick answer. For example, even with context, who can easily explain this randomly selected example:

```
(\W\*)(\W\*)[0,2,5]@
(\[yahoo(hotmail|)gmail\]\).com\W\*$
```

Personally, I'd take half a minute or so and re-enter the expected effort. Since regexes are worth constructing only when you use the same search repeatedly. In addition, you almost always will find scanning fuzzy logic results quicker than entering a lengthy regex, even if you type the regex correctly the first time. With *fzf*, you interact with the tool through a fuzzy logic interface, while *fzf* composes the regexes for a search behind the scenes.

Fuzzy logic is a science of its own, with principles and theories about communication and logic that do not directly concern us here [2]. What matters is that fuzzy logic is a much simpler way of introducing variation into output, especially today when the patience and general command-line knowledge among computer users is much less than it was 70 years ago. For one thing, the order in which variation is found with fuzzy logic is less important than with regexes.

Often, the order does not matter at all, which makes it easier to understand and more flexible. Just as importantly, fuzzy logic uses natural language instead of its own code that needs to be carefully separated from the query itself. If you add an indexed database, as *fzf* does, you can add context to accuracy to produce a contextual command history.

With these advantages, *fzf* has rapidly gained ground in the past few years. It is carried in all the major distributions, or it can be installed from its GitHub page. Each time *fzf* opens using the bare command, it updates its database in a matter of seconds, leaving you at a prompt, ready to continue.

![](img/e3f454b04d121b3b3750fddfda8dd21e_31_0.png)

![](img/e3f454b04d121b3b3750fddfda8dd21e_32_0.png)

## Table 1: Keyboard Shortcuts

| Shortcut | Function |
| :--- | :--- |
| Ctrl+T | Select files |
| Alt+C | Switch into a selected subdirectory |
| Ctrl+R | Use *fzf*’s enhanced history |

## Setting Up *fzf*

The popularity of *fzf* means that, for most purposes, you can install it directly from your distribution’s repositories and begin to use it. You can also install *fzf* with Homebrew to get the absolute latest version.

However, to make full use of *fzf*, you should also install bat (the modern cat replacement) and fd-find (the modern find replacement). Then add the following lines to your _.bashrc_ files:

```bash
export FZF_DEFAULT_OPTS="--preview 'bat' \
	--color:always {:}"
export FZF_DEFAULT_COMMAND="fd -type f"
```

These lines will ensure that *fzf* can use bat as a file previewer and improve overall performance with fd-find. Faster than find, fd-find will ignore directories like _.gitignore_ while searching. In addition, add

```bash
source ~/.vim/share/fzf/shell/key-bindings.bash
```

to enable some useful keyboard shortcuts (see Table 1).

## Basic Use

At its simplest, *fzf* opens and updates its list of top-level directories for the present working directory – usually, your home directory. You can then type any part of a directory or file to see the results (Figure 1). If you scroll the results, highlighting and pressing the Enter key displays the selection in the terminal, where it can be conveniently pasted into newly typed commands. Alternatively, you can use *fzf* with another command so that

```bash
: vim $(fzf)
```

allows you to use *fzf* to select a file to open in Vim.

For many uses, this is enough information to use *fzf*. However, depending on how *fzf* is compiled, it can also support context-specific autocompletions by entering a command followed by **\*+Tab** and will give appropriate suggestions, such as file names for Vim or remote systems for SSH. If autocompletion is not enabled, check the project’s GitHub page for instructions.

## Other Command Options

Most online articles on *fzf* end at this point. However, a few distributions, such as Ubuntu, offer man pages with additional options, neatly organized into categories. Among the most immediately useful are the search modes. Some of these options may be familiar to you from find and other search commands. For instance, with **\*1**, searches become case-sensitive, while you can reduce clutter in the results with –exact. In addition, –ai=**g**\*TYPE sets the fuzzy algorithm, completion with v1 optimizes speed over best results, and v2 optimizes results over speed.

Another useful option category is for search results. The arrangement of results can be influenced by –t{left}=**CfI** {CRITERIA, CRITERIA}. The default criteria is length, which favors shorter results, but you can give it lower priority by its position in a list that can contain begin (with the search string closer to the start of the line), end (with the search string closer to the end of the line), or index (a line that already appears in the results). Each criterion should only appear once, and index (for obvious reasons) must always appear last. If you are searching for high-level directories, start might be a useful option or end if you are searching for a file name. In addition, –tac displays results in reverse order.

Other options are cosmetic, such as disabling the mouse or horizontal or vertical control, or aspects of appearance, such as color theme or window border size for previews. These options no doubt become more important the more often you use *fzf*, but at first glance give a false sense of complexity for what is after all a relatively well-organized utility.

## Rough Edges

The latest version of *fzf* is 0.38, and many distributions offer even earlier packages. Unsurprisingly, *fzf* is still rough around the edges, with no indication of what features are compiled in which package or distribution and scanty documentation. Fortunately, though, you do not need all the possible features to find *fzf* a major improvement in search functions. In fact, *fzf* has several levels of complexity, each of which is useful in itself. As a result, even with the general release apparently some way off, *fzf* is a welcome innovation that is well on the way to becoming the new norm in search commands. **▮▮**

### Info

- 1. fzf: https://origin-sysadmin.redhat.com/fzf-linux-fuzzy-finder
- 2. Fuzzy logic: https://en.wikipedia.org/wiki/Fuzzy\_Logic
