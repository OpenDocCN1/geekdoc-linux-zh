
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

- 32.3.1 Perusing Text from the Web Perusing text from the Web.
- 32.3.2 Viewing a Site That Requires Authorization Browsing sites which require logging in.
- 32.3.3 Options Available while Browsing Text Lynx startup options.

## 32.3.1 Perusing Text from the Web

To peruse just the text of an article that's on the Web, output the text of the URL using `lynx` with the `--dump` option. This dumps the text of the given URL to the standard output, and you can pipe this to `less` for perusal, or use redirection to save it to a file.

- To peruse the text of http://www.sc.edu/fitzgerald/winterd/winter.html, type (all on one line):

```
$ lynx --dump http://www.sc.edu/fitzgerald/winterd/winter.html | less RET
```

It's an old net convention for italicized words to be displayed in an etext inside underscores like `_this_`; use the `--underscore` option to output any italicized text in this manner.

By default, `lynx` annotates all the hyperlinks and produces a list of footnoted links at the bottom of the screen. If you don't want them, add the `--nolist` option and just the "pure text" will be returned.

- To output the pure text, with underscores, of the previous URL, and save it to the file `winter_dreams`, type (all on one line):

```
$ lynx --dump --nolist --underscore http://www.sc.edu/fitzgerald/winterd/winter.html > winter_dreams RET
```

You can do other things with the pure text, like pipe it to `enscript` for setting it in a font for printing.

- To print the pure text, with underscores, of the previous URL in a Times Roman font, type (all on one line):

```
$ lynx --dump --nolist --underscore http://www.sc.edu/fitzgerald/winterd/winter.html | enscript -B -f "Times-Roman10" RET
```

> *NOTE:* To peruse the plain text of a URL with its HTML tags removed and no formatting done to the text, see Converting HTML to Another Format.

## 32.3.2 Viewing a Site That Requires Authorization

To view a site or Web page that requires registration, use lynx with the `-auth` option, giving as arguments the username and password to use for authorization, separating them by a colon (`:`) character.

- To view the URL http://www.nytimes.com/archive/ with a username and password of `cypherpunks`, type (all on one line):

```
$ lynx -auth=cypherpunks:cypherpunks http://www.nytimes.com/archive/ RET
```

It's often common to combine this with the options for saving to a file, so that you can retrieve an annotated text copy of a file from a site that normally requires registration.

- To save the URL http://www.nytimes.com/archive/ as an annotated text file, `mynews`, type (all on one line):

```
$ lynx -dump -number_links -auth=cypherpunks:cypherpunks http://www.nytimes.com/archive/ > mynews RET
```

NOTE: The username and password argument you give on the command line will be recorded in your shell history log (see section Command History), and it will be visible to other users on the system should they look to see what processes you're running (see section Listing All of a User's Processes).

## 32.3.3 Options Available while Browsing Text

The following table describes some of the command-line options lynx takes.

| OPTION | DESCRIPTION |
|---|---|
| -anonymous | Use the "anonymous ftp" account when retrieving ftp URLs. |
| -auth=user:pass | Use a username of user and password of pass for protected documents. |
| -cache=integer | Keep integer documents in memory. |
| -case | Make searches case-sensitive. |
| -dump | Dump the text contents of the URL to the standard output, and then exit. |
| -emacskeys | Enable Emacs-style key bindings for movement. |
| -force_html | Forces rendering of HTML when the URL does not have a `.html` file name extension. |
| -help | Output a help message showing all available options, and then exit. |
