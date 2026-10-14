To help you begin on the right track, the following sections provide overviews of key X principles. After that, I explain each step of a sample program that demonstrates common X programming techniques. Learn these basics, and you’ll find it much easier to absorb and understand the examples in the coming chapters. Knowing Xlib fundamentals also makes it relatively easy to learn how to use higher-level X toolkits.

> Note Readers with some X experience can skip the rest of this section and go directly to "Introducing Xlib Programming." However, I urge all to read through the following overviews for a better understanding of the example programs that follow.

# A Few Good Terms

Following are some critical X terms and phrases used in this and the other chapters in this part. While learning about X programming, you might want to mark this section for future reference.

API An Application Programming Interface, or API, provides functions, and often structures and other data declarations, for operating system software. For example, Xlib is the API for X development. Xlib provides functions that X applications can call to perform various actions such as displaying text and graphics in a window.

Child window A child window is one that another parent window owns. Except for the root window, every X window is a child of a parent window. See also Parent window, Root window, and Window.

Client In general terms, under the client/server model, a client requests data or services from server software. Typically, the client and server are separate tasks that might run at different locations on a network, an arrangement otherwise known as distributed processing. In X, however, the client/server model works a little differently. An X client is another name for an application—for example, a game or a word processor. The X client might run locally on the user’s system, or it might run on another system over a network. A client might be shared by multiple users, and it might communicate with more than one X server. The window manager is itself a client application. See also Client/server, Server, and X server.

Client/server This term describes the relationship between the X server and one or more client applications. All X installations, whether operating on a standalone workstation or across a network, are based on the X client/server model. See also Client, Server, and X server.

Colormap X uses one or more colormaps to relate hardware display capabilities with the values that programs can use to specify visual colors. By using colormaps instead of directly specifying colors—for example, as red, green, and blue values or as grayscale intensities—X clients can display information correctly regardless of the display’s characteristics. As a data structure, a colormap’s internal format depends on the nature of the