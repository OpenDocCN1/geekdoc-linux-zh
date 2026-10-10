The first few directories (the ones beginning with capital letters, taking advantage of the Unix convention of alphabetizing capital and lowercase initial letters separately, in accordance with the ASCII character set) are structural elements of the ports system, adjuncts that make the system work. The rest of the directories are categories of ports. Look inside one and you'll see as many as hundreds of different port directories, as demonstrated in Listing 14.5.

# **LISTING 14.5**  Ports Within a Category (Directory)

```
```
# ls -sF /usr/ports/audio/
total 230
1 Maaite/                  1 mpg123/
5 Makefile                 1 mpg123_el/
11 README.html             1 mpg321/
1 afsf/                    1 mpf20/
1 amp/                     1 mq3/
1 ascd/                    1 musicbox/
1 amix/                    1 musicbrainz/
1 aureal-kmod/             1 mutemix/
1 autozen/                 1 mvx/
1 bladeenc/                1 napster/
```
```

Browsing the ports in this way is less than efficient, especially in the larger categories. That's what the README.html file is for. Remember the “short description” that each package had? That description is stored in this file, too, and there's a README.html file at both levels of directories, as well as inside (almost) every port directory. You can browse the structure in hypertext using any Web browser on the local machine: Netscape, if you're using the machine as an X-Windows workstation, or lynx if you're logged in remotely (as shown in Figure 14.3).

![](bbox=[0.33, 0.67, 0.68, 0.82])

# **FIGURE 14.3**  Browsing a category's README.html file in lynx.