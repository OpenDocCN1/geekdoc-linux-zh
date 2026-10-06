
## Chapter 19 ✦ Running Bootable Linux Distributions 501

project is probably a good place to start if you want to produce a LiveCD that is compatible with either of those distributions. There are currently more than a dozen LiveCD distributions that have been created from the LiveCD project.

Of the projects I've just mentioned, I'd recommend starting with a KNOPPIX or Damn Linux distribution for your first attempt at remastering. Because there are a lot of people using those, or other distributions based on Debian/KNOPIX technology, there are mature procedures and forums to help you get over any bumps in the road.

## Summary

Dozens of bootable Linux distributions have appeared in the past few years. Those distributions can contain anywhere from 1.4MB of data on a firewall bootable Linux to many gigabytes of data on a bootable DVD. Without needing to touch the computer's hard disk, these distributions can offer full-featured systems that are tailored to desktop systems, multimedia players, rescue systems, or many other types of systems.

Many bootable Linuxes are based on KNOPPIX (described in Chapter 11), so they feature very fine hardware detection and strong network connectivity. If you want to try out a mini-bootable Linux distribution, try Coyote Linux (described in Chapter 17).

Nearly all bootable Linux distributions offer ways to access data from the hard disks of the computers on which they are running. While many bootable Linuxes are all experimental in nature, you have lots of fun playing with them. With the extraordinary improvements in custom features, you can create your own customized bootable Linux distribution to take with you on a floppy, CD, DVD, or USB flash drive (also referred as pen drives, thumb drives, or other names).

## Running Applications

In This Part

- **Chapter 20** Playing Music and Video
- **Chapter 21** Working with Words and Images
- **Chapter 22** E-Mailing and Web Browsing
- **Chapter 23** Gaming in Linux

## CHAPTER 20

## Playing Music and Video

### In This Chapter

- Legal issues with digital media
- Using your Windows content on Linux
- Playing music
- Setting up TV and audio cards
- Recording and ripping music
- Watching TV and videos

One of the most popular and enjoyable activities on a computer is playing audio and video. With improved multimedia tools and players for storing and managing content, Linux has become a great platform for storing, playing, and managing your music and video files.

In this chapter, you will learn to use the sound, video, digital imaging, and other multimedia tools available for Linux. You explore the process of configuring audio and select devices and examine the media formats available for the Linux platform, how they work, and how to make the most of them using the right applications.

Linux is an excellent platform for taking advantage of widely used formats such as MPEG, AVI, OGG, and RealMedia. A wide variety of players are available for the various formats, and this chapter discusses several of them to help you determine which might be the right one (or combination) for your interests and needs.

> While many devices holding multimedia content are removable (CDs, DVDs, digital cameras, Webcams, and so on), recent features in Linux to automatically handle removable hardware and media have greatly improved the Linux desktop experience. See the section on managing hardware in Chapter 4 for descriptions of how features such as Udev and HAL are used to manage removable media.

## Playing Digital Media and Obeying the Law

Debate about just what an end user can legally do with digital media is a hot topic right now. What exactly can you do as far making copies of your CDs, DVDs, and other media?

Part IV ♦ Running Applications

Unfortunately, there is no really good answer. This issue affects just about every computer user, either directly or indirectly.

How are you allowed to use the audio, video, and other media you keep on your computers is increasingly dictated by law (U.S. and international). There was a time when you could essentially disregard this issue, but in the era where individual computer users have been successfully sued by corporations and industry groups, a little more caution is required.

## Copyright Protection Issues

The biggest factor in the new world of digital media policy is the 1998 Digital Millennium Copyright Act (DMCA). This law ostensibly establishes a framework for implementing several international treaties concerning copyright protection.

The DMCA has been widely criticized because it seems to intrude on the free-speech provisions of the U.S. Constitution. Many people view computer code as a protected form of speech. A conflict arises because the DMCA forbids the development of applications that are intentionally to circumvent content security. Dmitry Skylarov, a Russian cryptographer employed by a Russian software company, ElcomSoft, was arrested by the FBI because he had demonstrated an application that could decrypt Adobe. A jury found Skylarov not guilty in December 2002, but the point is that companies still use the DMCA to litigate against those who publish methods to decrypt encrypted content.

If nothing else, this event demonstrated that the DMCA had teeth. Unfortunately, these teeth have been used only to protect commerce, but to pursue computer scientists at academic institutions researching content protection schemes, encryption, and a range of other technologies. Because the DMCA makes it a crime to manipulate and transport technology to circumvent copyright protection schemes, many researchers have abandoned valuable research that could yield better (stronger and more useful) protection schemes or reveal critical flaws in existing ones.

While DMCA has provided some clout for content providers to legitimately protect them, the DMCA is very vague how it defines many of the acts that are illegal. (Wait, correcting logic flow) Because the DMCA makes it a crime to manipulate and transport technology to circumvent copyright protection schemes, many researchers have abandoned valuable research that could yield better (stronger and more useful) protection schemes or reveal critical flaws in existing ones.

While DMCA has provided some clout for content providers to legitimately protect their material, the DMCA is very vague how it defines many of the acts that are illegal. What is a “protection scheme?” Some argue that it could be nearly anything. Many pundits fear that the DMCA can be used to curtail the use of nondirectional copyrighted works such as books because the law is vague in defining its bounds.

While the courts are trying to clarify what the legal line is in any particular situation, there's a problem in that often, the company seeking to protect its copyrights is a large corporation or the defendant is a new company or an individual user. and the broad scope of the DMCA essentially prevents the “little guy” from making his case, because he cannot afford to.

> In 1998 a law known as the Sonny Bono Copyright Term Extension Act or CTEA was passed. This act actually the lengthy copyright protection period (generally 70 years) and extended it by another 20 years, preventing several valuable properties, including film and images of Steamboat Willie (the first Mickey Mouse), from entering the public domain.

The question of practicality is very important when examining copyright issues. In other words, what does this mean to you as a Linux user? Well, it means that you have to use any trickery to copy MP3s off your CD collection, you could be breaking the law.

While DMCA has provided some clout for content providers to legitimately protect their material, the DMCA is very vague how it defines many of the acts that are illegal. (Wait, re-merging based on OCR flow)

- Users can make a copy of any work for academic purposes, reporting or critique. But what about the student making a copy of the DVD
- Fair-use rule is a principle that permits someone other than the owner of the copyright to use the material in a reasonable and limited manner.
- Users can sell copyrighted works that they own. You can sell books, DVDs, audio, and other materials as long as you are not retaining a copy for yourself, or (of course) selling copies of the work without permission.
- Copyright will expire at time in the future and fall into the public domain. This point raises the same issue as the first item: Your DVD movie enters the public domain (eventually), but to freely copy the content you may circumvent the protection inherent on the DVD and by doing so, you run of all of the DMCA.

- Users can make a copy of any work for academic purposes, reporting or critique. But what about the student making a copy of the DVD own- Fair-use rule is a principle that permits someone other than the owner of the copyright to use the material in a reasonable and limited manner.
- Users can sell copyrighted works that they own. You can sell books, DVDs, audio, and other materials as long as you are not retaining a copy for yourself, or (of course) selling copies of the work without permission.
- Copyright will expire at time in the future and fall into the public domain. This point raises the same issue as the first item: Your DVD movie enters the public domain (eventually), but to freely copy the content you may circumvent the protection inherent on the DVD and by doing so, you run of all of the DMCA.

(Note: The OCR text at the end had some significant repetitions/fragmentation due to page breaks. I have cleaned up the logical flow based on the provided segments.)

Wait, let me provide the clean, merged version of the text without my internal meta-notes.

[content]
## Chapter 19 ✦ Running Bootable Linux Distributions 501

project is probably a good place to start if you want to produce a LiveCD that is compatible with either of those distributions. There are currently more than a dozen LiveCD distributions that have been created from the LiveCD project.

Of the projects I've just mentioned, I'd recommend starting with a KNOPPIX or Damn Linux distribution for your first attempt at remastering. Because there are a lot of people using those, or other distributions based on Debian/KNOPIX technology, there are mature procedures and forums to help you get over any bumps in the road.

## Summary

Dozens of bootable Linux distributions have appeared in the past few years. Those distributions can contain anywhere from 1.4MB of data on a firewall bootable Linux to many gigabytes of data on a bootable DVD. Without needing to touch the computer's hard disk, these distributions can offer full-featured systems that are tailored to desktop systems, multimedia players, rescue systems, or many other types of systems.

Many bootable Linuxes are based on KNOPPIX (described in Chapter 11), so they feature very fine hardware detection and strong network connectivity. If you want to try out a mini-bootable Linux distribution, try Coyote Linux (described in Chapter 17).

Nearly all bootable Linux distributions offer ways to access data from the hard disks of the computers on which they are running. While many bootable Linuxes are all experimental in nature, you have lots of fun playing with them. With the extraordinary improvements in custom features, you can create your own customized bootable Linux distribution to take with you on a floppy, CD, DVD, or USB flash drive (also referred as pen drives, thumb drives, or other names).

## Running Applications

In This Part

- **Chapter 20** Playing Music and Video
- **Chapter 21** Working with Words and Images
- **Chapter 22** E-Mailing and Web Browsing
- **Chapter 23** Gaming in Linux

## CHAPTER 20

## Playing Music and Video

### In This Chapter

- Legal issues with digital media
- Using your Windows content on Linux
- Playing music
- Setting up TV and audio cards
- Recording and ripping music
- Watching TV and videos

One of the most popular and enjoyable activities on a computer is playing audio and video. With improved multimedia tools and players for storing and managing content, Linux has become a great platform for storing, playing, and managing your music and video files.

In this chapter, you will learn to use the sound, video, digital imaging, and other multimedia tools available for Linux. You explore the process of configuring audio and select devices and examine the media formats available for the Linux platform, how they work, and how to make the most of them using the right applications.

Linux is an excellent platform for taking advantage of widely used formats such as MPEG, AVI, OGG, and RealMedia. A wide variety of players are available for the various formats, and this chapter discusses several of them to help you determine which might be the right one (or combination) for your interests and needs.

> While many devices holding multimedia content are removable (CDs, DVDs, digital cameras, Webcams, and so on), recent features in Linux to automatically handle removable hardware and media have greatly improved the Linux desktop experience. See the section on managing hardware in Chapter 4 for descriptions of how features such as Udev and HAL are used to manage removable media.

## Playing Digital Media and Obeying the Law

Debate about just what an end user can legally do with digital media is a hot topic right now. What exactly can you do as far making copies of your CDs, DVDs, and other media?

Unfortunately, there is no really good answer. This issue affects just about every computer user, either directly or indirectly.

How are you allowed to use the audio, video, and other media you keep on your computers is increasingly dictated by law (U.S. and international). There was a time when you could essentially disregard this issue, but in the era where individual computer users have been successfully sued by corporations and industry groups, a little more caution is required.

## Copyright Protection Issues

The biggest factor in the new world of digital media policy is the 1998 Digital Millennium Copyright Act (DMCA). This law ostensibly establishes a framework for implementing several international treaties concerning copyright protection.

The DMCA has been widely criticized because it seems to intrude on the free-speech provisions of the U.S. Constitution. Many people view computer code as a protected form of speech. A conflict arises because the DMCA forbids the development of applications that are intentionally to circumvent content security. Dmitry Skylarov, a Russian cryptographer employed by a Russian software company, ElcomSoft, was arrested by the FBI because he had demonstrated an application that could decrypt Adobe. A jury found Skylarov not guilty in December 2002, but the point is that companies still use the DMCA to litigate against those who publish methods to decrypt encrypted content.

If nothing else, this event demonstrated that the DMCA had teeth. Unfortunately, these teeth have been used only to protect commerce, but to pursue computer scientists at academic institutions researching content protection schemes, encryption, and a range of other technologies. Because the DMCA makes it a crime to manipulate and transport technology to circumvent copyright protection schemes, many researchers have abandoned valuable research that could yield better (stronger and more useful) protection schemes or reveal critical flaws in existing ones.

While DMCA has provided some clout for content providers to legitimately protect their material, the DMCA is very vague how it defines many of the acts that are illegal. What is a “protection scheme?” Some argue that it could be nearly anything. Many pundits fear that the DMCA can be used to curtail the use of nondirectional copyrighted works such as books because the law is vague in defining its bounds.

While the courts are trying to clarify what the legal line is in any particular situation, there's a problem in that often, the company seeking to protect its copyrights is a large corporation or the defendant is a new company or an individual user. and the broad scope of the DMCA essentially prevents the “little guy” from making his case, because he cannot afford to.

- Users can make a copy of any work for academic purposes, reporting or critique. But what about the student making a copy of the DVD?
- Fair-use rule is a principle that permits someone other than the owner of the copyright to use the material in a reasonable and limited manner.
- Users can sell copyrighted works that they own. You can sell books, DVDs, audio, and other materials as long as you are not retaining a copy for yourself, or (of course) selling copies of the work without permission.
- Copyright will expire at time in the future and fall into the public domain. This point raises the same issue as the first item: Your DVD movie enters the public domain (eventually), but to freely copy the content you may circumvent the protection inherent on the DVD and by doing so, you run of all of the DMCA.

> In 1998 a law known as the Sonny Bono Copyright Term Extension Act or CTEA was passed. This act actually the lengthy copyright protection period (generally 70 years) and extended it by another 20 years, preventing several valuable properties, including film and images of Steamboat Willie (the first Mickey Mouse), from entering the public domain.

The question of practicality is very important when examining copyright issues. In other words, what does this mean to you as a Linux user? Well, it means that you have to use any trickery to copy MP3s off your CD collection, you could be breaking the law.
