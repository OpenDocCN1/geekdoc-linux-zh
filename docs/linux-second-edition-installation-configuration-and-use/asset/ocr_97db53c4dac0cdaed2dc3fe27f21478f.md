# Colors

The preset colors of strn occasionally make it impossible to read the text. A slight modification works wonders: the following line causes headings (in the help text too) to be displayed in blue on a white background.

color headers blue

# Mouse control

With the following line, many functions of strn can be controlled via the mouse:

```
set mouse 1
```

Besides menu control and selection of groups or individual news articles, there are a number of not so obvious mouse shortcuts.

# strn mouse shortcuts

In the 'News Group' status line:

+   - Left button scroll list forward
- Right button scroll list backward
- Middle button close list view

In the article status line:

+   - Left button jump to the next unread news article
- Right button jump to the previous unread news article
- Middle button view/hide quoted text (> > text)

In the article text:

+   - Left button scroll text forward
- Right button scroll text backward
- Middle button close text view

# tin

tin is a handy program which may leave you with a rather meager first impression, but which is actually much more efficient in its handling than some other programs (such as Netscape). With strn: do not be deterred by the very simple interface!

# Start

Just like strn, tin too evaluates the contents of the environment variable NNTPSERVER or the file /etc/ntpserver, where the name of the news server must be specified (for example localhost or news.provider.de). Alternatively, the server name can be specified with the option -g.