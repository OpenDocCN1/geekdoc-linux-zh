The next line, which was added to `sources.list`, enables `apt-get` to search a third-party repository (but see the following security tip):

```
deb http://download.skype.com/linux/repos/debian/ stable non-free
```

In this case, the repository is named `stable` and the category is `non-free`. Although the code is compiled for Debian, it runs on Ubuntu, as is frequently the case.

# Use repositories you trust

There are many repositories of software packages. Be selective regarding which repositories you add to `sources.list`. When you add a repository, you are trusting the person who runs the repository not to put malicious software in packages you might download. In addition, unsupported packages might conflict with other packages or cause upgrades to fail.