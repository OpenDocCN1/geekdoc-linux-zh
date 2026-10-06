previously in the chapter and a variety of other sources of information Essentially this is a useful way to bring together many of the various sources of information installed on the system and to view the documentation in one place. The Help Center is searchable; the first time you attempt a search it will build an index under /var/cache/susehelp/. Figure 5-5 shows what the Help Center looks like.

# /usr/share/doc/packages/

Many packages on the system at least some related documentation in the directory /usr/share/doc/packages/. Occasionally, badly behaved third-party packages will use /usr/share/doc/packages/. The quality of the documentation found here varies. In many cases you will simply find a copyright notice and installation instructions that are irrelevant because they apply to installing and building from source. However, some packages install serious documentation here in the form of print manuals in PostScript or PDF format. For example, if you install the unison package (a file synchronization program), you will find a /usr/share/doc/packages/unison/unison-manual.ps that is a 56-page PostScript manual for the program, which you can print or view with gv or kgview.

![](bbox=[0.181, 0.465, 0.816, 0.853])

Figure 5-4: Konqueror displaying the info page for du