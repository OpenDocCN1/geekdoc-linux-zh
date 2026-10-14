# pr – Format Text For Printing

The pr program is use to paginate text. When printing text, it is often desirable to separate the pages of output with several lines of whitespace, to provide a top and bottom margin for each page. Further, this whitespace can be used to insert a header and footer on each page.

We’ll demonstrate pr by formatting our distros.txt file into a series of very short pages (only the first two pages shown):

```
[me@linuxbox ~]$ pr -l 15 -w 65 distros.txt

2008-12-11 18:27                 distros.txt                 Page 1

SUSE      10.2   12/07/2006
Fedora    10     11/25/2008
SUSE      11.0   06/19/2008
Ubuntu    8.04   04/24/2008
Fedora    8      11/08/2007

2008-12-11 18:27                 distros.txt                 Page 2

SUSE      10.3   10/04/2007
Ubuntu    6.10   10/26/2006
Fedora    7      05/31/2007
Ubuntu    7.10   10/18/2007
Ubuntu    7.04   04/19/2007
```

In this example, we employ the -l option (for page length) and the -w option (page width) to define a “page” that is sixty-five columns wide and fifteen lines long. pr paginates the contents of the distros.txt file, separates each page with several lines of whitespace and creates a default header containing the file modification time, filename, and page number. The pr program provides many options to control page layout. We’ll take a look at more of them in the next chapter.