![](bbox=[0.07, 0.09, 0.62, 0.36])

Figure 3: Homebrew has a complicated series of names that reflect the contents of each directory.

As with many package managers,
these eight commands are enough for most user interactions with Homebrew. However, Homebrew also has a lengthy man page that for some reason is not installed with it [6]. Some of the options are specific to developers creating formulae, such as the spellcheck type-check command or the analytics command for repositories, and will not be discussed here for lack of space, but a number are also useful for convenience or administration purposes. For example, among the convenient options are completion, which autocompletes typed commands once enabled for a Bash, Zsh, or fish shell by linking to online dictionaries [7]. Similarly, home or homepage, qualified by a formula’s or cask’s name, opens to the target’s web page so you can learn more about them. In addition, once you have mastered Homebrew’s jargon, there are sub-commands and options for dealing with formulae in groups, instead of individually.

The administrative options include a number of options that help keep a system current. For instance, cleanup action uses the --prune DAYS option to remove files in Homebrew’s cache that are older than a certain number of days or -s to remove the cache entirely. Another potentially useful action is outdated, which lists formulae for which a newer version is available. This is especially useful when accompanied by the action migrate, which takes options for when a formula’s name is changed in a newer version, or bump, which sets whether an older version should be updated.

# A Nice App

Homebrew is a comprehensive package manager. Despite the fact that it is only 13 years old, in many ways it is as far-reaching as the much older apt-get or Yum. It even includes features that could be useful in other package managers. However, access to Homebrew’s advanced features is partially blocked by unnecessary jargon. As well, while its formulae must number in the thousands, they are nowhere near, for instance, Debian’s 60,000 packages. It is only in the Ruby on Rails community that Homebrew is likely to dominate. For the rest of us, these notes should be enough to use Homebrew when a developer decides to use it, with a minimum of fuss and only a slight loss of convenience. ■■■

# Info

+   [1] Homebrew: [https://brew.sh/](https://brew.sh/)
+   [2] Install Homebrew: [https://docs.brew.sh/Installation](https://docs.brew.sh/Installation)
+   [3] How to Install and Use Homebrew on Linux: [https://www.digitalocean.com/community/tutorials/how-to-install-and-use-homebrew-on-linux](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-homebrew-on-linux)
+   [4] Common issues: [https://docs.brew.sh/Common-Issues](https://docs.brew.sh/Common-Issues)
+   [5] Jargon and formulae: [https://docs.brew.sh/Formula-Cookbook#homebrew-terminology](https://docs.brew.sh/Formula-Cookbook#homebrew-terminology)
+   [6] Man page: [https://docs.brew.sh/Manpage](https://docs.brew.sh/Manpage)
+   [7] Shell completion: [https://docs.brew.sh/Shell-Completion](https://docs.brew.sh/Shell-Completion)