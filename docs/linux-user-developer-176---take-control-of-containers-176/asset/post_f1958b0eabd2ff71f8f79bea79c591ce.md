
## Python column

nobody can seem to remember. Over time, you may find that not all of the installed packages are needed any more. This could be an issue on a small machine like the Raspberry Pi. The first step is to clean up the Berryconda environment. You can remove unused versions of packages, cached installation tarballs of the packages in the environment, and index caches. Assuming that you simply want as lean a system as possible, you can clean up the entire environment with the following command:

```bash
conda clean --all
```

If there are installed packages that are no longer needed, you can remove them with the uninstall command. For example, the following command would remove the scipy Python module:

```bash
conda uninstall scipy
```

If you have a drastic need to restart, you could remove everything from the environment by using the `--all` command option.

One of the great strengths of Python is the large set of third-party modules available for extending functionality. Unfortunately, this is also one of its weaknesses, leading to a large amount of garbage building up over time. The Python module `virtualenv` was written to try to deal with this issue. The conda packaging system also understands creating isolated Python environments. This way, you can have the best of both worlds: easier Python module management combined with easier Python environment management. You can get a list of all of the environments conda knows about with the following command:

```bash
conda env list
```

If you have just installed Berryconda, the only environment listed is the root environment. Now, let's say that you needed to start a new code base, developing the software for a big new project. You could create a new empty environment with the following command:

```bash
conda create --name deatistar
```

This command creates a new subdirectory within the envs subdirectory inside the Berryconda environment. If you rerun the environment list command, you will now see both the root environment and the deatistar environment, with the latter tagged on by an asterisk as the currently active one. You can now install only the modules you require for this specific software project by activating it and running the usual conda commands. For example, the following commands would install ipython, along with all of its dependencies, within the deatistar environment.

```bash
source activate deatistar
conda install ipython
```

You can leave a given environment by running the deactivate script to reset all of the environment variables. If you have already put together a basic environment that you want to use as a starting point for a new environment, you can clone it as your boilerplate. The clone option to the create command comes in handy for such a task.

```bash
conda create --name deatistar2 --clone deatistar
```

If the reason for your software project goes away, you can always clean up old environments with the remove command in conda.

```bash
conda remove --name deatistar --all
```

The command option `--all` ensures that all portions of the environment are deleted during the removal process.

Now, you should have all of the information you need to be able to work in isolated environments for your Raspberry Pi projects. This is especially useful in the development stages of a new project. You can get only the modules you need for a given project.

## Raw virtualenv

While the conda system is a very powerful tool in simplifying the management of environments and Python modules, it isn't the only one available. As mentioned in the main article, there is the `virtualenv` module available to do the same basic task. You can install it with the command:

```bash
sudo apt-get install virtualenv
```

It will also install a number of dependencies. The main command is called `virtualenv`. With it, you can create new environments, manage them and even delete unneeded ones. To create a new environment, you can use the following command:

```bash
virtualenv deatistar
```

This will create a new subdirectory, named deatistar, within the current directory. It then makes a copy of the core of a Python Environment, including Python itself and setup tools like pip. There is also a set of management scripts available within the newly created environment. In a similar fashion to conda environments, you can activate the "deatistar" environment with the following command:

```bash
source ./deatistar/bin/activate
```

Once you activate the new environment, any Python module you install will be installed within this environment's directory structure. For example, if you install scipy with the command:

```bash
pip install scipy
```

...all of the files associated with the scipy module will be installed within the lib subdirectory of the environment. Depending on what versions of pip and setuptools are initially available when you created your new environment, you may need to update them before installing any new modules. If you run into any issues, start with the following two commands before diving too deeply into debugging:

```bash
pip install -U pip
pip install -U setuptools
```

This gives you another option if you don't want to deal with the full conda system.

## BUILD A BETTER WEB

www.webdesignermag.co.uk

![](img/6866071e033820549b214c239744aaa0_81_0.png)

# web designer

- EVERY ISSUE
- FREE RESOURCE DOWNLOADS

Available from all good newsagents and supermarkets

# ON SALE NOW

- Industry interviews | Expert tutorials & opinion | Contemporary features | Behind the build

![](img/6866071e033820549b214c239744aaa0_81_1.png)

# BUY YOUR ISSUE TODAY

Print edition available at www.imagineshop.co.uk
Digital edition available at www.greatdigitalmags.com

- Available on the following platforms
- Print Tablet Phone Desktop
- facebook.com/webdesignermag twitter.com/webdesignermag

## Reviews

83 Group test | 88 Synology RT2600ac | 90 AryaLinux 2017 | 92 Free software

![](img/6866071e033820549b214c239744aaa0_82_0.png)

**GROUP TEST**

### Password managers

Keeping the details of your accounts safe is of more importance than ever before, but which open-source password manager is worth investing your time in?

**Clipperz**
Security is key when it comes to Clipperz, which is why it claims to know nothing about its users or the data they choose to encrypt. Through passphrases and vault options, Clipperz looks to offer everything a user could need to keep their virtual presence safe.
Clipperz.com

**Passopolis**
While most password managers are tailored to individuals, Passopolis uses a friend-based system where users are able to invite certain people to access their account. It’s a unique feature, but does the program have a whole lot enough to stand out from some fierce competition?
Passopolis.com

**Encryptr**
Considering Encryptr comes from the team who produce the amazing Spideroak secure cloud server, Encryptr has a pretty impressive history. It prides itself on its simplicity to attract new users, while not skipping on the staple elements that every password manager needs.
Spideroak.com

**KeePass**
Consider KeePass the old man of the group, and a program that many seasoned Linux users will recognise. It’s undergone some big changes as of late, with improvements made to both the UI and expanding on what used to be a fairly limited set of features.
Keepass.info

## Review

### Password managers

### Clipperz

> Anonymity is key when it comes to using Clipperz's vault system

![](img/6866071e033820549b214c239744aaa0_83_0.png)

Different tags can be applied to each entry you make within Clipperz

#### UI and design

Thanks to its minimal UI system, navigating through Clipperz is a breeze. Individual vault entries are categorised through keywords, which are then accessible through the side menu; although some didn't save correctly at times. Each password entry can be cloned and archived when needed, a nice touch if you've got several closely linked accounts.

#### Adding and customising entries

Large amounts of details can be attached to each entry, especially when it comes to debit and credit card information. As you create passwords, Clipperz will indicate any password that it feels needs to be updated, even providing examples for what makes a good password. However, the constant reminders of how rubbish our passwords were soon became tiresome!

#### Security

Instead of storing readable data on their server, they use a host-proof web app that instead encrypts and decrypts the data inside Clipperz. This is great news for users, as it makes it near impossible for your entries to be compromised from their side. There's also 128-bit encryption board, which automatically adds two-step authentication at any point where Clipperz deems it necessary to use.

#### Extra features

One of Clipperz's best features is its one-time password system, which allows for secure access to your files from an insecure device. It works a treat, and especially useful when you need instant access when out and about. There's also a mobile version for users to explore, but it lacks many of the core features that the desktop version offers.

#### Overall

Clipperz does everything it sets out to do relatively well, and we truly believe your details will be safe. Certain features are a little rough around the edges, but expect that to be sorted in future updates.

8

### Passopolis

> Is sharing the key to success for Passopolis?

![](img/6866071e033820549b214c239744aaa0_83_1.png)

Changes to your passwords can be made at any time

#### UI and design

While some will be attracted to Passopolis's minimal design, it's a little too bonebones for our liking. Most options are available through its on-board account system, but some are hidden away and pretty difficult to find unless you're familiar with the software. However, a handy search tool is available for quickly sifting through your entries.

#### Adding and customising entries

Known as 'secrets' in Passopolis, adding new entries is a one-button process. Details can be added as you see fit, but it does lack the customisability of what Clipperz offers. However, we did like the team-based entries that can be created, allowing you to share access to specific entries with pre-targeted family and friends when needed.

#### Security

Although there's nothing truly unique about the security protocols used within Passopolis, it does include everything that you could need. A password generator is on hand for adding custom passwords, while users also have access to two-factor authentication when needed. Exporting files does require a decryption run-through first, which can take a while to complete, however.

#### Extra features

Again, there's not a lot to get excited about here. There's an import system on hand, however. If you're moving from your previous manager across to Passopolis, you can have your entire vault of entries imported with relative ease. Be warned, this isn't a quick process, and a full import can take anywhere from a few minutes to a couple of hours.

#### Overall

Sticking to the basics is all well, and good, but Passopolis tends to feel a little too minimal at times. A lack of customisation on entries is an annoyance, but all base options are present.

6

84
