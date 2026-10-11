
## How About a Little Flash? Shocking!

Before we wrap up, let's revisit that Export dialog one more time. Click File from the menu and select Export. When the Export dialog appears, have another look at the File format selection box, just below the File Name field. The default is to export to an HTML document, but there are other options here. For one, we have a PDF export; the one-button export (beside the printer icon on the standard bar) is common to Impress as well.

Notice as well that you have a Macromedia Flash export capability. Isn't that interesting? Enter a filename for your presentation (no need to add the .swf extension). With a single click of the Export button, your presentation is saved to Macromedia's Flash format. Now, your presentation is viewable from any browser with a Macromedia Flash or Shockwave plugin. The advantage of this over the HTML export is that all your animated slide transitions are preserved. Visitors to your site can view the presentation as it was intended.

## So What's with the Penguin?

Having made you run off to Larry Ewing's site for a copy of Tux, I suppose I should take a moment to answer one of the most frequently asked questions in the Linux world. After all, every time you look at a Linux book, boxed set, or Web site, you stand a good chance of coming face to face with a fat, smiling penguin. You may well be wondering what Linux has to do with this penguin (see Figure 15-14). Well, for starters, his name is Tux, and he is the Linux mascot. The most famous version of Tux (and there are many) is Larry Ewing's design.

![](img/0e9cf4c65a042f4a9bea644dc50153a7_297_0.png)

The story behind Tux is the stuff of legend now and, like most legends, a little hard to pin down. Linus Torvalds was asked what he envisioned for a mascot. The answer from Linus was, "You should be imagining a slightly overweight penguin (*), sitting down after having gorged itself, and having just burped. It's sitting there with a beatific smile—the world is a good place to be when you have just eaten a few gallons of raw fish and you can feel another 'burp' coming."

There is also another story where Linus claims he was attacked by a killer penguin at the Canberra Zoo, where he contracted "penguinitis," a disease whose main symptom is that you "stay awake at nights just thinking about penguins and feeling great love towards them."

That's the thing about legends. They tend to get strange over time.

> Some people have told me they don't think a fat penguin really embodies the grace of Linux, which just tells me they have never seen an angry penguin charging at them in excess of 100 mph.
> They'd be a lot more careful about what they say if they had.
>
> —Linus Torvalds

# Extra! Extra!

Before we move away from the classic office applications, I would like to take another moment to address the issue of templates. Although StarOffice, the nonfree commercial sibling of OpenOffice.org, comes with a number of templates for word processing, spreadsheets, and presentation graphics, OpenOffice.org is still quite *light* in this area. As I mentioned earlier, the Impress package includes only a couple of templates.

To that end, I'm going to remind you of the Web sites I mentioned at the end of Chapter 13. They are Travis Bauer's OOOExtras site and Scott Carr's OpenOffice.org Documentation Project. Both are excellent starting points for adding to your collection of templates. Look for the links to both in the Resources section.

Perhaps, in time, you too will contribute to this growing body of work.

## Alternatives

In the last two chapters, I mentioned that the KDE office suite, KOffice, offers similar components that you may want to consider. These include KWord for word processing and KCalc for spreadsheets. There's also an alternative for presentation graphics and that is KPresenter. As before, you can use Synaptic to search for and install KOffice. Remember that you do not need to be running KDE to run KOffice or any of its components. These applications work very nicely from the GNOME desktop.

## Resources

- **KPresenter**
  `http://koffice.kde.org/kpresenter/`
- **Larry Ewing's "Tux" (the Official Linux Penguin)**
  `http://www.isc.tamu.edu/~lewing/linux/`
- **Linux Logo Links at Linux.org**
  `http://www.linux.org/info/logos.html`
- **OOExtras**
  `http://ooextras.sourceforge.net`
- **OpenOffice.org Web Site**
  `http://www.openoffice.org/`
- **OpenOffice.org Documentation Project**
  `http://documentation.openoffice.org`

# Chapter 16 OpenOffice.org Base

![](img/0e9cf4c65a042f4a9bea644dc50153a7_301_0.png)

Computers have thousands of uses, but in the end, the most important things they do come down to two major and equally important functions. The first is mathematics. More specifically, the computer makes it possible to do complex (or simple) mathematics quickly. The key word here is quickly. Whether it is figuring out ballistics tables to better ensure the trajectory of a missile and cracking complex codes (as was the impetus for the computer's development during World War II) or processing a company's financial information, math is central to every computing operation.

The second most useful function a computer has is storing, sorting, and retrieving data quickly. (Again that word quickly.) Search engines like Google or Yahoo! are a testament to the computer's power of sifting through large amounts of information. In doing so, businesses can locate a customer's address in seconds, even though there may be millions of other customer records in the system. A hospital with thousands of patient records can pull up your medical history in a flash and update it with today's visit. The online bookstore maintains your personal information so you can buy a book with a click or two. A year's worth of financial information, arranged into a clear, concise report, appears on the printer seconds after the company accountant requests it.

As my wife, Sally, is fond of saying, “It’s all about the data.”

Storing data, or information, if you prefer, is what a database is all about. That’s why the addition of a database into the OpenOffice.org suite is so exciting. OpenOffice.org Base makes it possible to create your own databases, retrieve and modify information, perform queries, create reports, and so on. Base can attach to an existing database engine such as Oracle, Microsoft Access, MySQL, and many others using ODBC or JDBC. If all you need your database to do is simple operations, such as creating and maintaining a mailing list, OpenOffice.org base comes with the built-in HSQL database engine.

## The Beginning: Creating a New Database

Because I mentioned mailing lists, let’s use that as the basis for our exploration of OpenOffice.org Base. When we are through creating the database, I’ll show you how to use it in another OpenOffice.org program, the Writer word processor. We’ll take the information from our mailing list and create mailing labels.

To start OpenOffice.org Base, click Applications in the top panel and select OpenOffice.org Base from the Office submenu (command name: oobase).

When you start OpenOffice.org Base, you are presented with the Database Wizard (see Figure 16-1). This is a simple wizard with only two screens, the first of which is to select or identify a database. Your options are to Create a New Database, Open an Existing Database File, or Connect to an Existing Database. Let’s just go ahead and create a new database by making sure that radio button is selected. Click Next.

The second step is where you must decide how to proceed after saving your database. There are only a few options on the second and final screen, but they are important and worth explaining (see Figure 16-2).

![](img/0e9cf4c65a042f4a9bea644dc50153a7_303_0.png)

Figure 16-1 The OpenOffice.org Base Database Wizard.

![](img/0e9cf4c65a042f4a9bea644dc50153a7_303_1.png)

Figure 16-2 The final step in the wizard registers the database so it is easily accessible by other OpenOffice.org applications.
