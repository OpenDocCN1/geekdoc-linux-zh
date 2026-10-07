# v.4.33 A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

being, these make for excellent tertiary cross-verification tools and vehicles for learning specific artifacts and structure.

# Registry Parsing #1 - UserAssist

Let's start our exploration of libyal'd and application analysis by looking at specific Windows registry files.

As usual, we start with the disclaimer that this section is not about learning registry forensics. It's about the tools. Of course you might gain some knowledge along the way, but if you want to go deeper into these registry files and learn more about the art of registry forensics, I strongly suggest you look to the excellent book³⁰ written by Harlan Carver (and browse his blog!). You might want to have a basic understanding of registry structure before you begin this exercise, so you have some context for what's to come. And, of course there are other (faster and more comprehensive) ways to parse. For example, Harlan Carver's well-known RegRipper will run just fine on Linux.

Our real purpose in this section is to show you how to do this analysis at the byte level, using some Linux tools like xxd and tr, rather than relying on automated tools to do it for you. What we do here is not much different from what the Perl scripts in RegRipper do (although we simplify it somewhat).

First, we need to have a registry file to work on. We'll start with the NTUSER.DAT file from the Albert account in our NTFS file system (NTFS_Pract_2017.E01).

We need to make sure we obtain the correct NTUSER.DAT. There are a couple of ways we can locate and extract the file from a disk image. You can mount the image (in our case using mount), browse to the file and copying it out of the mounted file system. This requires a few more steps than we need to do, so we'll demonstrate it here with two simple location methods, and then extract the file with icat.

Since we are the Albert account, and we know that a specific user's NTUSER.DAT file is in the /Users/$USERNAME/ folder, we can use find to target the specific file by name. To run find, we use mmls as we did previously to find the offset to the file system in our image:

> ³⁰https://www.elsevier.com/books/windows-registry-forensics/carvey/978-1-59749-580-6

> ³¹https://www.windowsir.blogspot.com/

286