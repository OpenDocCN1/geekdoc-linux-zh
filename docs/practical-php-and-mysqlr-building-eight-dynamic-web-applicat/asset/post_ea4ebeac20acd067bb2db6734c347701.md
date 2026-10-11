
## Administering Projects
398

## Changing General Settings
406

## Managing Downloads
407

## Deleting Releases
414

## Managing Screenshots
415

## Deleting Images
419

## Adding a New Project
420

## Deploying the Application
421

## Summary
424

# CHAPTER 11
## Building a News Web Site

### Project Overview
425

### Installing PEAR Packages
426

### Building the Database
428

### Starting to Code
431

### Handling User Logins
440

### Viewing and Rating Stories
445

### Managing Stories
451

### Managing Categories
457

### Creating Your Search Engine
461

### Summary
467

# APPENDIX A
## Web Site Design

### Project Overview
469

### Laying Out the Site
471

### Starting to Code
474

### Start Build the Stylesheet
479

### Formatting the Main `<div>` Items
481

### Creating an About Page
487

### Creating a Frequently Asked Questions Page
489

### Formatting Tables
492

### Summary
495

# Index

# Foreword

Listen to podcasts by Jono Bacon and friends at LUG Radio (www.lugradio.org) and you get a sense of both the spirit and thoughtfulness Jono brings to the open source community. At one moment they speak seriously about hurdles in contributing code to free software projects, while the next they offer a Monty Python-like discussion on which Linux distribution each of them most resembles.

*Practical PHP and MySQL* reflects Jono’s commitment to the spirit of making open source subjects accessible to everyone. The book carefully walks you through the code for eight useful, dynamic Web applications. Projects are presented in a playful way, like the forum project that touts horror movies that make you “hide behind the couch.” And everything in the book can be run live, modified, saved, and reused from the included live CD.

Although the tools you need to create Web content are readily available from the open source community, having a skillful guide like Jono Bacon to help you create dynamic Web applications from those tools is a real treat. The results form a foundation for developing your own blogs, forums, shopping carts, and other Web destinations that should significantly cut your startup time.

I am thrilled to have Jono Bacon’s *Practical PHP and MySQL* as one of the first books in the Negus Live Linux Series. Its content perfectly suits the goals of the series to put quality free and open source software covering various topics into peoples’ hands so they can quickly get high-quality results. I hope you enjoy learning from this book as much as I have.

—Christopher Negus

**Series Editor, Negus Live Linux Series**

# About the Author

**Jono Bacon** works for Canonical as the Ubuntu community manager and is an established speaker, author, and regular contributor to the Open Source community. As an author, Bacon co-authored *Linux Desktop Hacks* and the *Official Ubuntu Book*, and has written more than 400 published articles in more than 14 publications. Bacon has also contributed as a columnist for *Linux Format*, *Linux User & Developer*, and *PC Plus*, and is an O'Reilly Network weblog author.

In addition, Bacon is a regular contributor to Open Source in a range of projects, a lead developer on the Jokosher (www.jokosher.org) project, and one of the co-founders of the popular LUGRadio (www.lugradio.org) podcast---a show with more than 15,000 listeners and an annual event that pulls visitors from around the world.

# Acknowledgments

Writing thank-you lists is always hard, because I always end up leaving out someone important. I want to give thanks to the following people for their incredible support and help:

- Susan Curtis, John and Pauline Bacon, Simon and Martin Bacon, Banger and Frankie, Prentice Hall (Debra Williams-Cauley, Songlin Qiu), LUGRadio (Stuart Langridge, Matthew Revell, Adrian Bradshaw), OpenAdvantage (Paul Cooper, Elliot Smith, Scott Thompson), #php, #mysql, and #lugradio on FreeNode, the LUGRadio community, Kai “Oswald” Seidler, and many more.

Everyone is going nuts about the Web. Ever since we started getting creaky old modems installed in our homes and businesses, the Web has become an increasingly dominant part of our lives. With it we explore, shop, diagnose, entertain, amuse, communicate, collaborate, and more. The Web is no longer a novelty item that the few use to stretch their technical muscles; millions of people all over the world are living their normal lives, with the Web playing a central role.

The popularity of the Web means interesting things for developers such as you. The Web has not only presented a means to develop information-rich resources such as IMDB, Wikipedia, and so on, but the Web also provides a real opportunity to create online applications for doing everyday things, such as managing contacts, balancing accounts, selling products or services, creating content, expressing opinions, chatting, and much more. A worldwide audience awaits, and if you have the technical chops, you can tap into this audience.

This is where PHP and MySQL swirl into play. In recent years, PHP and MySQL have come together to form a unique and awesomely powerful platform. With their roots in Open Source, these entirely free tools can be used to create hugely functional, stable, enterprise-class Web sites. We can wax lyrical about PHP and MySQL later, so let's talk about what this book can do for you.

# A DIFFERENT APPROACH

If you walk into the vast majority of bookstores and look for programming books, they all use approximately the same format. These books tend to progressively and linearly ramble through the subject and present a series of facts. This approach is
