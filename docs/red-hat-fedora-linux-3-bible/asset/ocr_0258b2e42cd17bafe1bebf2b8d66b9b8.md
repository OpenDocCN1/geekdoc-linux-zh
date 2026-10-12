to be immediately transported to another Web page (or other content) by simply selecting a linked text string or image on the page.

The primary tool for displaying HTML Web pages is the Web browser. Mozilla is the most popular Web browser for Fedora Core. Mozilla's Firefox, however, is quickly gaining ground. Both display HTML (Web pages) as well as other types of Web content. Now, even file managers, made for displaying local files and folders, have been extended to be able to display Web content (see the description of Konqueror file manager in Chapter 3).

This section contains general information about the Web and some specific hints for using Mozilla to browse the Web from your Fedora Core system.

# ## Uniform Resource Locators

To visit a site on the Internet, you either type a URL into the location bar on your browser or click on a link (either on a Web page or on a menu or button on the browser). Although URLs are commonplace these days — you can find them on everything from business cards to cereal boxes — you may not know how URLs are constructed. The URL form is as follows:

```
```
protocol://host-domain/path
```
```

The protocol identifies the kind of content that you are requesting. By far, the most common protocol you come across is Hypertext Transfer Protocol (HTTP). HTTP is the protocol used to request Web pages. In addition to HTTP, however, there are other protocols that might appear at the beginning of a Web address. Instead of showing you a Web page, these other types of protocols may display different kinds of information in your browser, or open a completely different application for working with the content.

Table 9-1 lists some of the protocols that can appear in a Web URL.

# ### Table 9-1: Protocols in Web URLs

| Protocol Name | Description |
| :--- | :--- |
| http | Hypertext Transfer Protocol. Used to identify HTML Web pages and related content. |
| file | Identifies a file on a specific host. Most often used to display a file from your local computer. |
| ftp | File Transfer Protocol. Identifies a location where there are file archives from which you might want to download files. |
| gopher | Gopher Protocol. Provides databases of text-based documents that are distributed across the Internet. (Gopher is nearly obsolete.) |
| mailto | Electronic Mail Address. Identifies an e-mail address, such as `mailto:joe@example.com`. (Usually opens a mail composer.) |
| news | USENET newsgroup. Identifies a newsgroup, such as `news://news.myisp.com/comp.os.linux.networking`. If you type this address into Mozilla, a window appears with the newsgroup displayed from the news server you identified. |