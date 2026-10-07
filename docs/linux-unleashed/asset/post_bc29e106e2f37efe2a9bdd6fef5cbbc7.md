
minimum by designing short Web pages, ideally with no scrolling required at all. Putting the demo software links at the top of the page makes them much more likely to get clicked on than something that requires scrolling or sorting through many icons at the bottom of the page.

## Using Multiple Pages

If you can’t fit everything that you need to say on the home page, by all means put auxiliary material on a link but make sure a reader doesn’t have to traverse too many links to find out what they want to know. If you’re trying to sell a product or service, for example, you don’t want a reader to have to go through five or six levels of links before they find out what you are offering and how much it is. The average reader just won’t last that long. A little advanced planning and some experimentation should result in a well laid out Web site. Remember to organize everything logically so that a visitor will be able to figure out your site’s layout quickly.

> **TIP**
>
> There are a couple of easy ways to draw a Web visitor’s attention to an item on your pages. The first is a simple horizontal rule (using the `<HR>` tag) across the page. Since the horizontal rule doesn’t impose any overhead to download, there’s no delay imposed by using it on your pages. Keep the number of horizontal lines low, though, to avoid overwhelming the reader.

## Using Icons

Icons are great for letting your readers know what is important on your home page. Unfortunately, too many Web page designers go nuts and have many different kinds of icons scattered all over the page. This just doesn’t work well—it distracts the reader and leads to confusion about which icons are important and which are not.

Bullets are a useful icon, as long as they are used with a short list that readers can quickly grasp. Again, go for something simple and attractive. Changing the bullet every item is confusing. The simplest icon for bulleted lists is a ball, although some browsers will add balls to bulleted lists if the list is tagged as an **HTML** list.

> **TIP**
>
> An attractive icon to point out important features can liven up a page. Clip art libraries are full of images like a point-right icon or a hand with a finger extended (be careful which finger!) to point to important items. These catch a reader's eye quickly.

A useful icon to point out potential items of trouble for readers is the warning, caution, or stop sign. The first two are usually a yellow triangle with an exclamation mark in them. These draw the reader's attention but should be used sparingly and only where a warning is necessary.

The “new” icon, in its many forms, is handy for highlighting something new to your page for those who visit regularly. Make sure the new icon really does apply to something new. Remove such icons after a couple of weeks so your page doesn’t seem stale.

## Use Links Properly

Links are the key to a good site, but they have to be carefully planned. Many Web site designers make a paper flow diagram of where each page and its links lead to in order to ensure the flow is logical, clean, and doesn’t cause silly loops anywhere. You should try to do this, too, if your site has more than three or four pages.

Choosing where to put the hyperlink itself is often a decision that Web page writers get mixed up with. For example, it’s not good to have a line like this:

Click here to see the latest releases

when it is much more descriptive and visually drawing to have this line:

Click here to find out about our latest releases

## Using HTML Tags Properly

Header tags are often misused by Web page designers. These use different size fonts to highlight titles. Keep the number of headline tags to a reasonable number and use them in order. After an `<H1>` tag use an `<H2>`, followed by `<H3>` and so on if applicable. Don’t skip a level and jump from `<H1>` to `<H3>`, as some browsers are starting to use these elements to structure outline views of pages.

Also avoid overlapping tags, where you change fonts or emphasis within each other. For example, the series

```html
<STRONG> Hello <EM> World! </EM> </STRONG>
```

may look fine on your browser but can cause problems on others. Always use tags in pairs and don't mix them.

Character tags should always be inside paragraph tags, not the other way around. For example, this is the proper way to nest character tags inside paragraph tags:

```html
<A HREF="Today's news">
    <UL>
        <LI>Added to the site today
        ...
    </UL>
</A>
```

Avoid using the `<BR>` tag to force word wrapping. Instead, let HTML do the wrapping for you or you may end up with lousy looking screens. Remember that just because the format looks good on your screen with your browser doesn't mean it will look good for all your visitors.

## Summary

Explaining all the principles of a solid Web page design in a few pages would be impossible. There are lots of good books on the subject. Do take care and create a clean, uncluttered site; otherwise, all your careful configuration and HTML work may be for nothing.

From here, there are a number of chapters you may want to read:

To learn about backups so you can recover your HTML code in case of a problem, see Chapter 45, “Backups.”

And to learn how to set up your Web server properly, see Chapter 51 “Configuring a WWW Site.”

To learn about source code control so you don't have multiple copies of your HTML documents floating around your directories, see Chapter 56, “Source Code Control.”

# Advanced Programming Topics

# PART VIII

## IN THIS PART

- Source Code Control 895
- Working with the Kernel 915
- Writing Device Drivers 927
- The Wine Project 939
- HylaFAX 955
- Games 965
- Adabas-D and other Databases 985
- StarOffice 999
- Lone Star Software's Lone-Tar 1007

# Source Code Control

by Peter MacKinnon and Tim Parker

## In This Chapter

- make 896
- RCS 905
- Retrieving version information from an RCS file 909
- Administering Access 910
- Comparing and merging revisions 910
- Tying it all together: working with make and RCS 912

A large-scale software project involving numerous files and programmers can present logistical nightmares if you happen to be the poor soul responsible for managing it:

“How do I know whether this file of input/output routines that Sue has been working on is the most current one?”

“Oh, no—I have to recompile my application, but I can’t remember which of these 50 files I changed since the last compile!”

Keeping track of which file is most recent and where you put those changes yesterday (or last week) can be more of a job than actual programming.

Even small applications typically use more than one source code file. When compiling and linking C applications, you usually must deal with not only source code, but also header files and library files. Fortunately, Linux features a software development environment that, for the most part, can greatly simplify these concerns.

## make

Perhaps the most important of all the software development utilities for Linux, make is a program that keeps a record of dependencies between files and only updates those files that have been changed since the last update. The term update usually refers to a compile or link operation, but it may also involve the removal of temporary files. This updating process can sometimes be repeated dozens of times in the course of a software project. Instead of managing these tasks manually, make can be your automatic dependency manager, giving you more time to do other important things, such as coding or watching TV.

make generates commands using a description file known as a makefile. These commands are then executed by the shell. The makefile is basically a set of rules for make to follow whenever performing an update of your program. These rules usually relate to the definition of the dependencies between files. In the case of creating a Linux executable of C code, this usually means compiling source code into object files and linking those object files together, perhaps with additional library files. make can also figure out some things for itself, such as the modification times (or timestamps) when certain files have been changed.
