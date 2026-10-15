
## INTRODUCTION

![](img/4ffb1cc24a1b24b49254839643abedb2_26_0.png)

A lot has changed in the world of Unix system administration since the first publication of this book in 2004. At that time, few casual computer users ran Unix-like operating systems—but as beginner-friendly desktop Linux distributions like Ubuntu gained popularity, that began to change. Then came OS X, the next iteration of Apple's Unix-based operating system, as well as a slew of technologies based on iOS. Today, Unix-like operating systems are more widely adopted than ever. Indeed, they are perhaps the most ubiquitous operating systems in the world, if we take Android smartphones into account. Needless to say, much has changed, but one thing that has persisted is the Bourne-again shell, as the prevailing system shell available to Unix users. Utilizing the full power of bash scripting has never been a more needed skill in a system admin's, engineer's, or hobbyist's toolbox.

## What to Take Away

This book focuses on common challenges you might face when writing portable automation, such as when building software or providing orchestration, by making common tasks easily automatable. But the way to get the most out of this book is to take the solution you create for each problem and extrapolate it to other, similar problems you may encounter. For instance, in Chapter 1, we write a portable echo implementation by creating a small wrapper script. While many system admins will get some benefit from this specific script, the important takeaway is the general solution of creating a wrapper script to ensure consistent behavior across platforms. Later on in the book, we delve into some wicked cool features of bash scripting and common utilities available for Unix systems, putting great versatility and power right at your fingertips.

## This Book Is for You If . . .

Bash remains a staple tool for anyone working on Unix-like servers or workstations, including web developers (many of whom develop on OS X and deploy to Linux servers), data analysts, mobile app developers, and software engineers—to name just a few! On top of that, more hobbyists are running Linux on their open source microcomputers, like the Raspberry Pi, to automate their smart homes. For all of these uses, shell scripts are perfect.

The applications of these scripts are endlessly useful for both those looking to develop their already substantial bash skills with some cool shell scripts and those who may only use a terminal or shell script every once in a while. Individuals in the latter camp may want to brush up on a few short cuts or supplement their reading with an introduction to more advanced bash concepts.

This book isn’t a tutorial, though! We aim to bring you practical technical applications of bash scripting and common utilities in (mostly) short, compact scripts, but we don’t provide line-by-line explanations. We explain the core parts of each script, and more seasoned shell scripters might be able to tell how the rest of the script works by reading the code. But we expect you as the reader to play with the script—breaking it and fixing it and altering it to meet your needs—to figure it out. The spirit of these scripts is all about solving common challenges, such as web management or syncing files—problems every techie needs to solve regardless of the tools they’re using.

## Organization of This Book

This second edition updates and modernizes the original 12 chapters and adds 3 new chapters. Each chapter will demonstrate new features or use cases for shell scripts, and together they cover a wide range of ways shell scripts can be used to streamline your use of Unix. OS X users should rest assured that most of the scripts in the book will work across Linux or OS X; it is called out explicitly when this is not the case.

## Chapter 0: A Shell Scripting Crash Course

This brand-new chapter for the second edition gives new Unix users a quick introduction to the syntax of bash scripts and how to use them. From the very basics of what shell scripts are to building and executing simple shell scripts, this short and no-nonsense chapter gets you up to speed on bash scripts so you can hit the ground running in Chapter 1.

## Chapter 1: The Missing Code Library

Programming languages in the Unix environment, particularly C, Perl, and Python, have extensive libraries of useful functions and utilities to validate number formats, calculate date offsets, and perform many other useful tasks. When working with the shell, we're left much more on our own, so this first chapter focuses on various tools and hacks to make shell scripts more friendly. What you learn in this chapter will help both with the scripts you find throughout the book and with your own scripts. We've included various input validation functions, a simple but powerful scriptable frontend to bc, a tool for quickly adding commas to improve the presentation of very large numbers, a technique for sidestepping Unices that don't support the helpful -n flag to echo, and a script for using ANSI color sequences in scripts.

## Chapters 2 and 3: Improving on User Commands and Creating Utilities

These two chapters feature new commands that extend and expand Unix in various helpful ways. Indeed, one wonderful aspect of Unix is that it's always growing and evolving. We're just as guilty of aiding this evolution as the next hacker, so this pair of chapters offers scripts that implement a friendly interactive calculator, an unremove facility, two reminder/event-tracking systems, a reimplementation of the locate command, a multi-time zone date command, and a new version of ls that increases the usefulness of the directory listings.

## Chapter 4: Tweaking Unix

This may be heresy, but there are aspects of Unix that seem broken, even after decades of development. If you move between different flavors of Unix, particularly between open source Linux distributions and commercial Unices such as OS X, Solaris, or Red Hat, you'll become aware of missing flags, missing commands, inconsistent commands, and similar issues. Therefore, this chapter includes both rewrites and frontends to Unix commands that will make them a bit more friendly or more consistent with other Unices. Included here is a method of adding GNU-style full-word command flags to non-GNU commands. You'll also find a couple of smart scripts to make working with various file compression utilities considerably easier.
