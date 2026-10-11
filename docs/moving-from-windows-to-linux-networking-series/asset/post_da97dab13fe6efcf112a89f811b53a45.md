
![](img/12d790664598bbf390261087fbe55bbc_249_0.png)

## Summary

In this chapter, we examined some of the extra applications that ship with Open Office. Perhaps the most important is the HTML Editor. We examined the basics of how to use this application to develop your own Web pages and discussed how to find free or low-cost Web hosting for your Web page. This information is of use to virtually any computer user.

We also took a look at how to change the Open Office settings using the Open Office Setup utility. It has a very user-friendly wizard that will enable you to change any settings you would normally set during installation.

## Review Questions

- 1. What is an image map?
- 2. How would you make a picture into a link to a Web site?
- 3. Name at least one free Web hosting site.
- 4. List three graphics types that you can insert into your Web page.
- 5. What is the purpose of the Open Office Setup utility?
- 6. What is the purpose of Open Office Math?
- 7. What is the purpose of Open Office Global?

![](img/12d790664598bbf390261087fbe55bbc_251_0.png)

## Answers

- 1. An image map is created when different regions of a single image link to different addresses.
- 2. Right-click on the picture to change its properties to include a link.
- 3. [www.angelfire.com](http://www.angelfire.com) and [www.geocities.com](http://www.geocities.com)
- 4. GIF, JPG, BMP
- 5. To alter options normally configured during the initial setup.
- 6. To provide a word processor for mathematical formulas.
- 7. To set up global parameters that are used throughout Open Office.

# Section IV: Important Linux Applications

## Chapter List

- Chapter 12: Moving from Adobe Photoshop to GIMP
- Chapter 13: Web Browsers, E-Mail, and Internet Applications
- Chapter 14: Miscellaneous Linux Applications
- Chapter 15: Web Servers in Linux
- Chapter 16: Linux FTP Servers
- Chapter 17: Fun and Games in Linux

This section will show you how to use several applications. There are a number of common tasks that you may have done in Windows and will probably want to continuing doing in Linux. The chapters in this section will show you the basics of a wide range of Linux applications. The section begins with an entire chapter on GIMP. GIMP is a very powerful graphics tool that will enable you to do professional digital image manipulation. The next chapter in this section shows you around various Internet utilities. You will learn how to use Linux Web browsers, chat clients, e-mail, and more.

Chapter 14 is a sort of smorgasbord. Many of the small applications and utilities that did not seem to fit anywhere else are covered here. Chapters 15 and 16 will show you how to set up your own Web server or FTP server. Finally, Chapter 17 shows you around the world of gaming in Linux. We will look at some of the games that install with Red Hat Linux, and we will discuss where to go on the Internet to find more Linux games.

# Chapter 12: Moving from Adobe Photoshop to GIMP

## Introduction

Like many Windows users, you probably have come to expect a lot of powerful graphics capability on your PC. Some Windows users are satisfied with the Paint and Photo Editor applications that come with Windows and are found under Accessories in the Programs menu. However, neither of these applications is a full-featured, robust, graphics package. Neither of these packages is of professional caliber. They are quite limited in what they enable you to do with an image. This of course leads to the question of what graphics application is of professional caliber? Many Windows users, as well as Macintosh users, turn to Adobe Photoshop as their choice for graphics applications. Adobe Photoshop is one of the most widely used graphics applications on the market today. It is hard to imagine anyone involved in graphics design, digital photography, or a related field who has not used Adobe Photoshop. However, there is no version of Photoshop available for Unix or Linux machines. It should also be pointed out that Adobe Photoshop is a commercial product and can cost several hundred dollars. Even if there were a version of Adobe Photoshop released for Linux (and as of this writing there are not even any hints or rumors to that effect), there is still another reason why you might want to search for an alternative product. If you are a home user, not a graphic artist, who wants a professional caliber program for your own use, it may seem unreasonable for you to pay several hundred dollars for a graphics application.

This is where GIMP comes in. GIMP is a graphics application that can do virtually everything that Adobe Photoshop can do. In fact, if you are experienced with Photoshop, you will probably be able to master GIMP within a matter of a few hours. The two applications are that similar. There are two real advantages to GIMP. The first is price. GIMP is open source and is available as a free download from [www.gimp.org](http://www.gimp.org). The second advantage is the platforms that GIMP is available for. GIMP was designed for Unix and Linux, but there is also a Windows version available. Much like Open Office, you can get GIMP for free and use it on both Windows and Linux machines.

## What Is GIMP?

GIMP is an acronym for General Image Manipulation Program. As we already mentioned, GIMP is an open source software application and is available free of charge. It was originally a project of Spencer Kimball and Peter Mattis, two students who were undergraduates at the University of California, Berkeley, when they created GIMP. It began as a project for one of their classes. They actually started out to write a LISP compiler. Frustration with the project caused the two students to move in a new direction. They decided to write an image manipulation project in C. The result has quickly grown into a full-fledged image editing program. As of this writing, GIMP releases are being orchestrated by Manish Singh. You can find out more on the history, current status, and future of GIMP by going to [www.gimp.org](http://www.gimp.org). You can also download your own copy of GIMP for Linux or for Windows from this Web site.

GIMP is a complete, fully functional graphics program. It is on a par with Adobe Photoshop and shares many features with that product. GIMP enables you to do professional-level graphics manipulation. It is ideal for a graphic artist, advertising professional, or any person that needs top-quality graphics. In this chapter we will examine using GIMP and walk you through the basics. If you followed the installation instruction in Chapter 2, "Installing Linux," then GIMP is already on your PC. If you did not, you can use the Packages option to add GIMP, or you can download it from the GIMP site.

## GIMP Basics

When you first launch GIMP, you will see a splash screen, shown in Figure 12.1. This screen is there to let you know the progress of GIMP in loading its various components and tools. How long this process takes depends on your computer. However, even on slow computers it is usually less than one minute. Of course, if you have several applications running simultaneously, this will slow things down quite a bit.

![](img/12d790664598bbf390261087fbe55bbc_255_0.png)

**Figure 12.1:** The GIMP splash screen.

Once the splash screen is done, you are shown a tip screen, depicted in Figure 12.2. There is a small check box on the bottom of this screen where you can elect to have tips show up at startup all the time. As a beginner it is probably a good idea to keep these tips showing. You will probably learn a lot about GIMP by reading these tips when learning GIMP. After you are more comfortable with GIMP, you can then decide to stop the tips from showing up every time you start GIMP.

![](img/12d790664598bbf390261087fbe55bbc_255_1.png)

**Figure 12.2:** The GIMP tip screen.

Once GIMP is running and you have made it past the splash screen and tip screen, you should immediately notice one major difference between GIMP and Adobe Photoshop. Photoshop, shown in **Figure 12.3**, has all the various tools together on one screen.

![](img/12d790664598bbf390261087fbe55bbc_256_0.png)

**Figure 12.3:** Adobe Photoshop.

GIMP has each set of tools in a separate window, shown in **Figure 12.4**. These windows can be moved or even closed in any manner you want. Some people find this layout a little confusing, but once you get used to it, you may come to realize that it provides you with a great deal of flexibility. You will find that many professional graphics programs choose this sort of layout. This is due to its flexibility. It enables the software user to place things in any way that he finds convenient.
