# Chapter 9: Using the Internet and the Web 361

+   - Konqueror — Although Konqueror is the file manager for the desktop, it can also display Web Content. Using Konqueror, you can easily go back and forth between Web sites and local folders and folders. A testament to the quality of Konqueror is that the Mac OS Safari browsers use the WebKit rendering engine, which is based on the Konqueror KHTMLML and kj engines.

If you are working from a shell, there are several command-line utilities that allow you to browse the Web without a graphical interface. These include the links, w3m, and lynx commands.

# Understanding Web browsing

Although the Internet has been around since the 1960s, the Web is a relatively new technology (ushered in by the creation of the first Web browser in 1990). The Web places an additional framework over Internet addresses that were limited to hostnames and domain. Before the Web, finding resources on the Internet was difficult. However, the Web now provides several features that make it much easier to access these resources:

+   - Uniform Resource Locators (URL)—URLs identify the location of resources on the Web. Besides identifying the domain and host on which a resource resides, you can also identify the type of content and the specific location of the content.

+   - Hypertext Markup Language (HTML) Web pages — When people talk about Web pages, they are generally referring to information that is presented in HTML format. HTML changed the Internet from a purely plain-text-based resource to one that can present graphics and font changes. An HTML page can also contain hyperlink links. Links are the threads that join together the Web, enabling viewing a Web page to be immediately transported to another Web page (or other content) by simply selecting a text string or image on the page.

The primary tool for displaying HTML Web pages is the Web browser. Firefox is the featured browser in Fedora and RHEL systems. It can display HTML (Web pages), as well as other types of Web. Now even file managers, for displaying local files and folders, have been enabled to display Web content (see the description of Konqueror file manager in Chapter 3).

This section contains general information about the Web and some specific hints for using different browsers (particular, Firefox) to browse the Web from your Fedora or RHEL system.

# Uniform Resource Locators

To visit a site on the Internet, you either type a URL into the location box on your browser or click a link (either from a menu or button on the browser). Although URLs are commonplace these days — you can find them everywhere from business cards to cereal boxes — you may not know how URLs are constructed. The URL format is as follows:

```
protocol://host-domain/path
```