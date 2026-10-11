
## Preface

“You may wonder, why a new edition of *Perl by Example*?” That’s how the preface for the fourth edition (2007) opened. So here we are again with a fifth edition and the twentieth anniversary since the first edition of *Perl by Example*, published in 1994. Same question: Why another edition? Perl 5 is still Perl 5.

First of all, a lot has been happening since the release of Perl 5.10. Many of the ideas from Perl 6 have been backported to Perl 5 as we await the official release of Perl 6. And as new features are added, there have been a number of incremental version changes, the latest version number being Perl 5.21. In fact, version 5.10 was what has been called the beginning of “modern Perl.” CPAN has added a number of new modules that have spiked interest in Perl, among them Moose, Mojolicious, Dancer, DBIx::Class, and more; and Core Perl has gained many modules as well, such as List::Util, Time::Piece, autodie, and so on. Those incremental changes to Perl 5 continue to enhance Core Perl and all the many new modules that deal with modern projects and technology. Perl 6 is still a work in progress. To see the roadmap for Perl 6 development, you can go to github.com or you can participate in the development process by going to perl6.org. But the fact is, we’re still entrenched in Perl 5 while we wait. This book addresses new features that have been added since the last edition, revitalizes and updates some of the older examples, and trims some of those topics that are not applicable in modern Perl.

As you read this, I am still teaching University of California, Santa Clara (UCSC) extension in Sunnyvale, California, to groups of professionals coming from all around Silicon Valley. I always ask at the beginning of a class, “So why do you want to learn Perl?” The predominant response today: for automation and testing, not CGI or bioTech, not even for completing a resume now that the Valley is on an upswing, but primarily for automation and testing. The legacy code remains for those companies that started with Perl, and it continues to grow. No matter what anyone tells you, Perl is still in demand. I know I teach it, not only at UCSC, but to those major companies that use Perl and require their employees to learn it as part of their training path.

Perl by Example is not just a beginner's guide but a complete guide to Perl. It covers many aspects of what Perl can do, from basic syntax to regular expression handling, files, references, objects, working with databases, and much more. Perl also has a rich variety of functions for handling strings, arrays, hashes, and the like. This book will teach you Perl by using complete, working, numbered examples and output with explanations for each line, and avoids veering off into other areas or using complicated explanations that send you off to your favorite search engine in order to figure out what's going on. It helps if you have some programming background, but it is not assumed that you are an experienced programmer or a guru. Anyone reading, writing, or just maintaining Perl programs can greatly profit from this text.

The appendices contain a complete list of functions and definitions, command-line switches, special variables, popular modules, and the Perl debugger; a tutorial to introduce Moose for object-oriented programming; a tutorial covering the Web application framework, Dancer, to replace the need for the Common Gateway Interface; and a guide for using PerlBrew and CPAN (“the gateway to all things Perl”) and how to effectively download modules.

I was fortunate to have been introduced to Alastair McGowan-Douglas as the technical expert for reviewing and critiquing this edition. He went well beyond the line of duty and has contributed greatly to not only transforming this book, but to adding his own writing for the tutorials in the appendices, correcting errors, and introducing modern Perl practices. His extensive knowledge and dedication have been invaluable. When we started the project, Alastair wrote to me:

> “… I should note that 'modern Perl' refers to the era since 5.10, where practices and conventions got a massive overhaul within the community, as Perl itself had a resurgence in development on it (the language and binary themselves). The previous edition, of course, predates this sea-change, which it seems like the rug has somewhat been swept out from under us.
> No matter! We shall prevail, as they say.”

And that is precisely what this edition has attempted to do!

—Elle Quigley
September 2014

## Acknowledgments

I’d like to acknowledge the following people for their contributions to the fifth edition.

Thank you, Mark Taub, an editor-in-chief to be praised for being very cool in every step of the process from the signing of the contract to the final book that you have now in your hand. Mark has a way of making such an arduous task seem possible; he soft-talks impossible deadlines, keeps up a steady pressure, and doesn’t get crazy over missed deadlines, quietly achieving his goal and always with a subtle sense of humor. Thank you, Mark, for being the driving force behind this new edition!

Of course, none of this would have been possible without the contributions of the Perl pioneers—Larry Wall, Randal Schwartz, and Tom Christiansen. Their books are must reading and include *Learning Perl* by Randal Schwartz and *Programming Perl* by Larry Wall, Tom Christiansen, and Jon Orwant.

Thank you, Vanessa Moore, the project manager and compositor who has been working with me for the past 20 years on making the *by Example* books look beautiful. She excels in her ability to do editing, layout, and artwork, and also in her ability to find errors that most programmers wouldn’t see, not to mention an abundance of patience and sense of humor. Without her, this book would be like a painting without color. She’s the best!

Also a big thanks to Daniel Holmes from NetApp (RTP) who contributed to the sections on Moose and wrote the final example; and Alastair McGowan-Douglas whose technical expertise was invaluable.

And last, but certainly not least, a huge thanks to all the students, worldwide, who have done all the real troubleshooting and kept the subject alive.

![](img/8556abcb353c0991f12099420ec28735_30_0.png)

# Chapter 1
## The Practical Extraction and Report Language

### 1.1 What Is Perl?

> "Laziness, impatience, and hubris. Great Perl programmers embrace those virtues."
> —Larry Wall

Perl is an all-purpose, open-source (free software) interpreted language maintained and enhanced by a core development team called the Perl Authors. It is used primarily as a scripting language and runs on a number of platforms. Although initially designed for the UNIX operating system, Perl is renowned for its portability and now comes bundled with most operating systems, including RedHat Linux, Solaris, FreeBSD, Macintosh, and more. Due to its versatility, Perl is often referred to as the Swiss Army Knife of programming languages.

![](img/8556abcb353c0991f12099420ec28735_30_1.png)

Larry Wall wrote the Perl language to manage log files and reports scattered over the network. According to Wikipedia, org, Perl was originally named "Pearl," but when Larry Wall realized that PEARL was another programming language that had been around since 1977, he simply dropped the "a" and the name became "Perl." Perl was later dubbed the Practical Extraction and Report Language, and by some, it is referred to as the Pathologically Ecclectic Rubbish Lister. Perl is really much more than a practical reporting language or eclectic rubbish lister, as you'll soon see. Perl makes programming easy, flexible, and fast. Those who use it, love it. And those who use it range from experienced programmers to novices with little computer background at all. The number of users continues to grow at a phenomenal rate.[^1]

[^1]: Perl is spelled "Perl" when referring to the language, and "perl" when referring to the interpreter.
