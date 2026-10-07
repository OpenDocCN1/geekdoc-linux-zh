Gopher is one of the most useful Internet services available because it is widely used by beginners and veterans alike. Gopher is a text-based file location system that leads you through a series of hierarchical menus to find specific files you want. Setting up a Gopher site is basically just a matter of configuring the Gopher server software and creating a number of logical directory structures with files indexed in a Gopher format.

Gopher works by having a client program (started by a user) connect to a Gopher server and retrieve information about files available on the Internet (or local area network, if the Gopher server is limited to that area). At the end of 1995, there were more than 6,000 Gopher servers on the Internet, all accessible by anyone with a Gopher client. Although the number has dropped a little since then (primarily because the World Wide Web has replaced some sites), there are still a lot of Gopher sites. Those servers contain information about more than 10 million items ranging from text files to movies, sounds, images, and many types of application binaries. Gopher enables you to display and manipulate lists of files, looking for items of interest to you.

If you or the users of your Linux system want to connect to another Gopher server, you need a Gopher client. There are several clients available with Linux distributions, on FTP and BBS sites, and through several other sources. If you don't want to allow users (or yourself) to start a Gopher client, you can use Telnet to connect to sites known as public Gopher clients. These sites allow you to log in as an anonymous user and access the Gopher system. Most Gopher client packages offer more than just Gopher programs. Typical Gopher clients enable you to access WAIS indexes, use FTP, and to some extent, interwork with the World Wide Web.

This chapter looks at how you can set up a Gopher server, allowing others to access your machine's Gopher listings. Although we won't go into detail about how you should structure your Gopher service, you will see how to configure your software.

# # Gopher and Linux

There are currently two versions of Gopher available for Linux systems: Gopher and Gopher+ (Gopher Plus). Gopher is freely available, but Gopher+ is a commercial product. The difference between the two is functionality. If the additional capabilities of Gopher+ are important to you and your Gopher site, you may want to consider purchasing the product. Essentially, Gopher+ adds the following features:

+   - Makes extended file information available
- Offers a description of a file