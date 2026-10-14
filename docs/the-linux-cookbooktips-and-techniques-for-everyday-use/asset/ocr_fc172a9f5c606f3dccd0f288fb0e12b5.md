interface for reading hypertext.

Type lynx to start it—if a "start page" is defined, it will load. The start page is defined in `/etc/lynx.cfg`, and can be a URL pointing to a file on the local system or to an address on the Web; you need superuser privileges to edit this file. On Debian systems, the start page comes defined as the Debian home page, http://www.debian.org/ (but you can change this, of course; many experienced users write their own start page, containing links to frequently-visited URLs, and save it as a local file in their home directory tree).

To open a URL, give the URL as an argument.

To view the URL http://lycaeum.org/, type:

```
$ lynx http://lycaeum.org/ RET
```

When in lynx, the following keyboard commands work:

| COMMAND | DESCRIPTION |
|---|---|
| @uparrow and @downarrow | Move forward and backward through links in the current document. |
| @rightarrow or RET | Follow the hyperlink currently selected by the cursor. |
| @leftarrow | Go back to the previously displayed URL. |
| DEL | View a history of all URLs visited during this session. |
| PgDn or SPC | Scroll down to the next page in the current document. |
| PgUp | Scroll up to the previous page in the current document. |
| = | Display information about the current document (like all pages in lynx, type @leftarrow to go back to the previous document). |
| g | Go to a URL; lynx will prompt you for the URL to go to. Type @uparrow to insert on this line the last URL that was visited; once inserted, you can edit it. |
| h | Display the lynx help files. |
| q | Quit browsing and exit the program; lynx will ask to verify this action. |

The following are some recipes for using lynx.

NOTE: Emacs users might want to use the `-emacskeys` option when starting lynx; it enables you to use Emacs-style keystrokes for cursor movement (see section Basic Emacs Editing Keys).

+   - 32.3.1 Perusing Text from the Web  Perusing text from the Web.
+   - 32.3.2 Viewing a Site That Requires Authorization  Browsing sites which require logging in.
+   - 32.3.3 Options Available while Browsing Text  Lynx startup options.