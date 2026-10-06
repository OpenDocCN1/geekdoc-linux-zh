
align with the project objectives. This is an evolutionary, not revolutionary change; by depending on and contributing to Open software since the inception of Red Linux, Red Hat has always shared control over the software with external developers. Red Hat will now more explicitly share control for packaging with external developers in our new project: The Fedora Project.

In June 2005, Red Hat announced its intention to form the Fedora Foundation by the end of August. Additional planning and application for 501(c)(3) non-profit status for the Fedora Foundation caused Red Hat to miss that date (although, I presume, the Fedora Foundation will have been formed by the time you read this text). The Fedora Foundation is expected to manage financial contributions and how code is managed by the Fedora Project.

## Listening to the Red Hat Community

As you might guess, the community of people who had hitched their wagons to the Red Hat train had some concerns about the Fedora/RHEL split. Some of the biggest concerns of the community are summed up by the following questions:

- **Is Fedora a real distribution?** Fedora has been set up for a project for shaking out software before that goes into Red Hat's commercial Linux products. Red Hat has gone to great lengths to make sure people know Red Hat is not guaranteeing or supporting Fedora. If that is the case, why would Red Hat care if Fedora is a fully integrated distribution once the parts it needs are enough to start up RHEL?

- **Who controls Fedora?** Right now, Red is calling all the shots when it comes to features, schedules, and other critical parts of Fedora. Input to discussions about Fedora and the formation of the Fedora Foundation have not yet significantly changed Red Hat's role is steering the project. Why would the community support a Linux system over which it has no control?

The funny thing is despite the confusing and frustrating aspects of the transition, many people in the open source community are still supporting the Fedora effort. I think that reality is an indication of how well regarded Red Hat's contributions to open source have been. The company is still generally trusted to offer some real value to the open source community as it also pursues its commercial agenda.

That said, I'll end this section with an excellent and (I believe) rather realistic reflection of how the transition to Fedora looked to the open source community. The following is a post to the Fedora-dev-list mailing list that includes a fictitious IRC session among the open source community, Fedora.us, and Red Hat, Inc. by Konstantin Ryabit. You can read the full post at http://lwn.net/Articles/83360.

## 284 Part III ♦ Choosing and Installing a Linux Distribution

Let me., err. relay how they are looking from outside of RH in the format everyone will understand...

```
BEGIN IRC LOG
<rh_pr> We are announcing Red Hat Project! A community-based distribution!
<oss_crowd> rh_pr: Neat. I'm not ready.
<rh_dev> rh_pr: Uh...
  * rh_pr is: promoting rh
<oss_crowd> rh_dev: what do we do?
<rh_dev> rh_dev: I'm not ready.
<rh_legal> rh_dev: don't do anything until I say it's.
<oss_crowd> rh_dev: what can we do with Red Hat Project?
<oss_crowd> rh_dev: uh... file bugs and help test things.
<oss_crowd> rh_dev: didn't we always do that?
<rh_sales> hey, all. if you really want a stable system, don't use fed project. It will eat your brain.
<rh_dev> rh_sales: stifi
  -- rh_pr removes voice from rh_sales
<fedora_us> hey, all. check out our community-driven for red development
<oss_crowd> fedora_us: ooooh!
<rh_pr> fedora_us: I like your name
  -- fedora_rh joined the channel
<rh_legal> much better
<rh_pr> We are announcing Fedora Project! A community-based distribution!
<oss_crowd> rh_pr: Neat!
  * fedora_rh waves
<fedora_us> I'm not dead yet.
<rh_dev> fedora_us: don't confuse things.
<fedora_us> rh_dev: does this mean we're merging?
<rh_dev> fedora_us: maybe
<rh_legal> rh_dev: don't do anything until I say it's.
<oss_crowd> fedora_us joined #limbo
<oss_crowd> rh_dev: so, what can we do to help?
<rh_dev> oss_crowd: uh... file bugs and help test things.
<oss_crowd> sigh... didn't we always do that?
<fedora_rh> oss_crowd: Know, let's all go in the circle and say our names:
  * oss_crowd grows in the circle and says their names. This lasts several months.
<rh_dev> So, there will be the following features in the next release of Fedora Core.
<oss_crowd> Uh... Then. Who gets to decide?
<rh_sales> We-do. That staff will be needed for RHEL-4.
<oss_crowd> MMay, then. When do_we get to suggest things?
<fedora_rh> oss_crowd: feel free to talk among yourself.
  * oss_crowd talks among themselves about new features.
<fedora_rh> btw, feature X will be disabled in the release.
  * oss_crowd glares at fedora_rh
```

## Chapter 8 ✦ Running Fedora Core and Red Hat Enterprise Linux 285

<oss_crowd> fedora_rh: nice to you tell us while we were sitting here talking,
<rh_dev> oss_crowd: sorry, it's just not happening.
<oss_crowd> rh_dev: when we get to decide what's happening?
<rh_dev> oss_crowd: Dunno, I'll ask rh_legal
<rh_legal> rh_dev: ugh, /msg
<rh_sales> rh_dev: let's not do anything rash here.
* fedora gets tired of sitting in #limbo
<oss_crowd> fedora_rh: I want to see more of the "community" part of the whole "community-based" thing
<oss_crowd> rh_dev: how at least publicly accessible CVS/SVN tree?
<rh_dev> oss_crowd: Yeah, that would be cool.
<oss_crowd> rh_dev: finally, some movement. When is that going to be up?
* rh_dev is away: talking to rh_legal
* oss_crowd tries to occupy themselves and does things like federanov and forspeople.
<oss_crowd> Uh... plng?
<fedora_uh> oss_crowd: what's up?
<oss_crowd> fedora_rh: We're feeling kinda useless. What exactly is our role, again?
<fedora_rh> oss_crowd: well, it would be really helpful if you could test some things and fix the files.
<fedora_rh> ugh. We ALWAYS did that.

```
- END IRC LOG
```

Even the fourth release of Fedora Core and many improvements to the Fedora Core distribution itself, there is still no certainty about its future.

## Installing Fedora Core

The Linux operating system Fedora Core, sponsored by Red Hat, is included in this book's DVD. The rest of this chapter leads you through its installation.

Before you install Fedora on your computer, ensure that your hardware supports it. You should also choose a method of installing Fedora. Those topics are discussed in the following sections.

## Choosing Hardware

Choosing your computer hardware may not really be a choice. You might just have an old PC lying around on which you want to try Fedora. Or you may have a workstation with some extra space and want to try Fedora on a separate partition or whole disk.

## 286 Part III ♦ Choosing and Installing a Linux Distribution

To install the PC version of Fedora (the accompanying DVD) successfully, the computer must have the following:

- **Processor:** The Pentium-class PC needs to be at least 200 MHz for text mode and 400 MHz for GUI.
- **RAM:** You need at least 64MB of RAM to install Fedora. If you are running graphical mode, you need 192MB. The recommended RAM for graphical mode is 256MB.
- **DVD or CD drive:** You need to be able to boot the installation process from a DVD or CD (the latter requires that you use Fedora CDs as described at http://fedora.redhat.com/download). If you cannot boot from a DVD or CD, there are ways to start the installation from a hard disk or using PXE install, as the following section "Installation Method," explains.
- **Hard disk:** Following is the required minimum disk space for five different installations. In each case, you will need to have more disk space than the minimums listed:

| Installation | Minimum Space |
| :--- | :--- |
| Personal Desktop | 2.3GB |
| Workstation | 3GB |
| Server | 1.1GB |
| Everything (Custom) | 6.9GB |
| Minimum (Custom) | 620MB |

- **Keyboard and monitor:** You need a keyboard and monitor at least during installation. (You can operate Fedora well over a LAN using either a shell interface from a network login or an terminal.)

To begin installing Fedora Core, you also need to have the Linux Bible DVD that comes with this book (or a set of installation CDs that you obtain yourself). Also you must be dedicating your entire hard disk (or an added hard disk) to Linux, have a preconfigured Linux partition, or have sufficient free space for your hard disk outside any existing Windows partition.
