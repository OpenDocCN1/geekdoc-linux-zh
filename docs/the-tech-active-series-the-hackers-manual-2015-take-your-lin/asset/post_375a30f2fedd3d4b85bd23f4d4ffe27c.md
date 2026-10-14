
Another serious issue is that the cloud service may be operated in a different country to your own, and therefore subject to a different legal framework and policies. Even if you are happy with the location, there is nothing to stop the cloud service provider moving everything to a data centre in a different country for economic or political reasons – or simply as a tax avoidance measure.

## One law for us, another for them

Google has come in for a lot of stick over its approach to privacy (not to mention its apparent consideration that paying tax is optional here in the UK) but Google isn’t alone in this, or even the worst offender. Google is simply the provider with the highest profile. To its credit, it is reasonably open about using your data to make money – most of us were aware that Google would read our emails before we signed up for a Gmail account.

Still, the idea of cloud services is appealing and convenient; so how do we resolve this dichotomy? The answer is simply to run your own cloud. That way, you get the convenience of easy access to your data from multiple platforms and locations but you retain control over that data. Now, we are not suggesting that you set up your own data centre to implement your own Gmail, Dropbox and Facebook, but you don’t need the scale of those organisations for a home or small business operation.

The cloud is basically built on top of the web, and Linux has something of a track record in providing web services. All you need is a Linux computer running the standard LAMP (Linux, Apache, MySQL, PHP) stack and you can install most of the software from the following pages in minutes. That just leaves two questions to answer: what and where. Depending on how much you want to do, the hardware could be a small server box, your desktop computer if you leave it switched on all the time – it may be needed – or even something really small and power efficient, like a Raspberry Pi or one of the plug computers. Any of these would be hooked up to your local network and so would give excellent speeds when used from within your LAN. They could also be made available from the outside, but then you run into the question of the upload speed of your internet connection. Most domestic internet connections are asymmetric, giving far higher speeds for downloads than uploads. But accessing data from the outside world counts as an upload, so it would be slower – not unusually so, but it’s something to be aware of, particularly if you want to support multiple users. If you are providing access from the world at large, life is a lot easier if your internet provider is able to give you a static IP address, otherwise you will need a dynamic DNS service.

## What do you need?

An alternative is a Virtual Private Server (VPS). This is a Linux distro running on a virtual machine at a data centre, so you get the benefit of the fast speeds such environments provide, but it’s still your own system and you control what software you include, and any passwords and encryption keys used, and the provider need not be able to read any of your data. You could also use a web host for this, because everything runs on a LAMP stack, but that reduces the options for protecting your data. Whatever the hardware you choose, real or virtual, you need a full LAMP installation. If you are devoting a box to the job, it is simplest to install on the server-oriented distros, like Ubuntu Server, or something like Debian and select the web server option when installing it. If you are using an existing system, installing Apache, MySQL and PHP should be sufficient. If you install the software we discuss from your distro’s package manager, it will take care of this for you.

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_20_0.png)

The demo at http://demo.owncloud.org lets you have a play around with ownCloud before installing it.

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_20_1.png)

The desktop sync client lets you set up multiple sync jobs to be run in turn – you’re not limited to one directory.

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_20_2.png)

The .tar archive is the classic way of installing ownCloud server. It provides the server and all the necessary 3rd party PHP libraries.

- Download Unix/Mac OS (.tar.bz2) or Windows (.zip) archive.
- Check package integrity using the MD5 sum. Unix/Mac OS / Windows.
- Follow the ownCloud Admin Manual’s installation chapter

Note: To receive information about updates and security issues, we recommend a subscription on our low-traffic announcement mailing list.

The website offers two ways of installing ownCloud, the simplest of these is to download and extract a tarball — unless your distro has a package for it.
