major flaws: Why do most libraries or frameworks built this way lack scalability? And Why do the libraries begin to look like a crazy quilt filled with swatches of different program snippets? The problem is simple: projects never have the big picture to help define the philosophy of a library. The best example of an over-overloaded class is MFC's CString class. To start a good, flexible, and clean library, the philosophy has to be defined first. Then you consider the possibilities for each class.

This section takes you through the process of fleshing-out the details of each class. The first and second steps are reversed when compared to normal object-project development.

# Attributes: Adding What It Knows

In most cases, the next step places the functions or methods in each class. However, when creating a library, especially a wrapper for the sockets API, you identify all the available features or attributes.

The socket's features are mostly built into the socket options. Chapter 9, "Breaking Performance Barriers," and Appendix A, "Data Tables," list the standard and Linux-dependent socket options. These are good candidates for the Socket class's attributes. In reality, the class does not keep the attributes as separate entries in the class. Instead, the socket descriptor holds each setting. Every get/set pair that normally accompanies the CRUD (Create/Read/Update/Delete) methods really calls getsockopt()/setsockopt().

Figure 13.5 shows the get/set function calls for each exposed attribute. Some attributes only turn on or off a feature, so the design does not include a get() function. A class may not expose all attributes; typically, the attributes that it exposes are those that change the behavior of the class. Other internal attributes may change only the state of the class, so they tend to remain hidden from view.

Figure 13.5. Each attribute in a class may have an associated get...() /set...() function.