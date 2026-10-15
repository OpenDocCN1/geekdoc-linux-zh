scripts can be used to streamline your use of Unix. OS X users should rest assured that most of the scripts in the book will work across Linux or OS X; it is called out explicitly when this is not the case.

# Chapter 0: A Shell Scripts Crash Course

This brand-new chapter for the second edition gives new Unix users a quick introduction to the syntax of bash scripts and how to use them. From the very basics of what shell scripts are to building and executing simple shell scripts, this short and no-nonsense chapter gets you up to speed on bash scripts so you can hit the ground running in Chapter 1.

# Chapter 1: The Missing Code Library

Programming languages in the Unix environment, particularly C, Perl, and Python, have extensive libraries of useful functions and utilities to validate number formats, calculate date offsets, and perform many other useful tasks. When working with the shell, we're left much more on our own, so this first chapter focuses on various tools and hacks to make shell scripts more friendly. What you learn in this chapter will help both with the scripts you find throughout the book and with your own scripts. We've included various input validation functions, a simple but powerful scriptable frontend to bc, a tool for quickly adding commas to improve the presentation of very large numbers, a technique for sidestepping Unices that don't support the helpful -n flag to echo, and a script for using ANSI color sequences in scripts.

# Chapters 2 and 3: Improving on User Commands and Creating Utilities

These two chapters feature new commands that extend and expand Unix in various helpful ways. Indeed, one wonderful aspect of Unix is that it's always growing and evolving. We're just as guilty of aiding this evolution as the next hacker, so this pair of chapters offers scripts that implement a friendly interactive calculator, an unremove facility, two reminder/event-tracking systems, a reimplementation of the locate command, a multi-time zone date command, and a new version of ls that increases the usefulness of the directory listings.

# Chapter 4: Tweaking Unix

This may be heresy, but there are aspects of Unix that seem broken, even after decades of development. If you move between different flavors of Unix, particularly between open source Linux distributions and commercial Unices such as OS X, Solaris, or Red Hat, you'll become aware of missing flags, missing commands, inconsistent commands, and similar issues. Therefore, this chapter includes both rewrites and frontends to Unix commands that will make them a bit more friendly or more consistent with other Unices. Included here is a method of adding GNU-style full-word command flags to non-GNU commands. You'll also find a couple of smart scripts to make working with various file compression utilities considerably easier.