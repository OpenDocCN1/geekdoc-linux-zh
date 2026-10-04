
# Chapter 12. Writing a Tcl Extension

Syntax: void Tcl_AddObjErrorInfo (interp, message, length)

Syntax: void Tcl_AddErrorInfo (interp, message)

Syntax: void Tcl_SetObjErrorCode (interp, objPtr)

Syntax: void Tcl_SetErrorCode (interp, element1, element2...NULL)

-   Tcl provides an interface to fast hash table database functions to allow tasks to save and retrieve arbitrary data based on keys.

-   A hash table must be initialized with the Tcl_InitHashTable
Syntax: void Tcl_InitHashTable (tablePtr, keyType)

-   Hash table entries may be manipulated with these functions:
Syntax: Tcl_CreateHashEntry (*tablePtr, key, newPtr)
Syntax: Tcl_FindHashEntry (tablePtr, key)
Syntax: void Tcl_DeleteHashEntry (entryPtr)

-   Data may be retrieved or deposited in a Tcl_HashEntry with these functions:
Syntax: ClientData TclGetHashValue (entryPtr)
Syntax: void Tcl_SetHashValue (entryPtr, value)

-   A match to a string can be found in an array of strings with the Tcl_GetIndexFromObj function.
Syntax: int Tcl_GetIndexFromObj (interp, objPtr, tblPtr, msg, flags, indexPtr)

-   The contents of Tcl variables can be accessed with these functions:
Syntax: Tcl_Obj *Tcl_ObjGetVar2 (interp, idlPtr, id2Ptr, flags)
Syntax: char *Tcl_GetVar2 (interp, name2, name1, flags)

-   The contents of Tcl script variables can be set with these functions:

Syntax: Tcl_Obj *Tcl_ObjSetVar2 (interp, id1Ptr, id2Ptr, newValPtr, flags)

Syntax: char *Tcl_SetVar2 (interp, name1, name2, value, flags)

-   A Tcl list is implemented with a Tcl object that contains an array of pointers to the elements of the list.

-   You can create a Tcl list within a C function with the Tcl_NewListObj function.
Syntax: Tcl_Obj* Tcl_NewListObj (count, objv)

-   You can get the length of a list with the Tcl_ListObjLength function.
Syntax: int Tcl_ListObjLength (interp, listPtr, lengthPtr)

-   You can retrieve the list element from a particular index in a list with the Tcl_ListObjIndex function.
Syntax: int Tcl_ListObjIndex (interp, listPtr, index, elementPtr)

# Extensions and Packages

The previous chapters described building Tcl packages and C language extensions to Tcl. Using these techniques, you can create almost any application you need.

In many cases your applications will need features that have already been developed. You can save time by using existing extensions and packages for these features. Using existing extensions not only saves development time but also reduces your maintenance and testing time.

This chapter provides an overview of a few extensions and packages. Unfortunately, it isn't large enough to cover all of the extensions and packages written for Tcl. The Tcl FAQ (frequently asked question) lists for over 700 extensions, and more are being written every day. Before you write your own extension, check to see if one has already been written.

The primary archive for Tcl extensions and packages is http://www.neosoft.com. The search engine at Ne will let you scan for a particular extension. Most extensions are also announced in comp.lang.tcl or comp.lang.tcl.announce. You can use the DejaNews PowerSearch engine (http://www.dejanews.com/home_ps.shtml) to limit your search to those newsgroups. Finally, many of the extensions are described in the Tcl/Tk FAQ (http://www.purl.org/NET/Tcl-FAQ).

Although extensions can save you a great deal of development time, there are some points to consider when using extensions and packages.

-   Extensions tend to lag behind the Tcl code. Most of these packages are developed by Tcl advocates who work in their spare time to maintain the packages. It can take weeks or months before they have time to update their package after a major change to the Tcl internals. In particular, the change from Tcl 7.6 to Tcl 8.0 introduced some API changes requiring rewriting that many extensions have not gone beyond version 7.6.

-   Not all extensions are available on all platforms. Many packages were developed before Tcl was available on Macintosh and Windows platforms, and they may have some Unix-specific code in them. As I am writing this book, several packages are being ported to other platforms. The extension descriptions list home pages where you can find out whether a package has been ported since this book was published.

-   Not all extensions are available at all sites. Installing extensions takes time, and keeping multiple versions of libraries and extensions consistent can create problems for system administrators. Thus, the more extensions your application requires, the harder it may be for users to install your application.

If you are writing an application for in-house use (and your system administrators will install the extensions you need), this is not a problem. If you write an application you'd like to see used throughout your company or distributed across the net, the more extensions it requires, the less likely someone is to be willing to try it.

If you need an extension, by all means use it. However, if you can limit a package to core Tcl or a single extension, you should do so.

-   Packages written in Tcl are more easily distributed than extensions written in C. Whereas many sites may not have an interest in running your Tcl application can run Tcl packages. You can include the Tcl packages your script needs with the distribution and install them with your application. For example, the HTML library discussed in Chapter 10 has been included in several other packages, including TclTutor, Surfelt, and wetk.

## 13.1 <incr Tcl>

This chapter will introduce these extensions:

-   <incr Tcl> The previous chapters have shown how object-oriented techniques can be used with pure Tcl. The <incr Tcl> is a true object-oriented extension of the Tcl core. It supports classes, private, public, and protected scopes, constructors, destructors, and inheritance.

-   expect Expect automates procedures that have a character-based interaction.

-   TclX This is a collection of new Tcl commands that support system access and reduce the amount of code you need to write. Many of the Tcl features have been integrated into recent versions of Tcl.

-   VS This package includes a database, a GUI generator, and a report generator. It's easy to set up and well suited to tasks that don't require a relational database server.

-   SybTcl SybTcl provides an interface to a Sybase database server.

-   OraTcl OraTcl provides an interface to an Oracle database server.

-   BLT A set of Tcl and Tk extensions that include support for treating numeric lists as high-speed vectors and creating graphs and bar charts.

-   Img, dash-patch These extensions increase Tcl's graphics and imaging capabilities. The dash-patch provides speedup and feature enhancements to the canvas widget, and the Img extension adds support for more image formats to the Tcl image object.

### 13.1 <incr Tcl>

Language C
Primary Site http://www.tclk.com/itcl/
Contact mmclennan@lucent.com, Michael McLennan
Tcl Revision Supported Tcl: 7.3-8.0 Tk: 3.6-8.0
Supported Platforms Unix, MS Windows, Mac 68K, Mac PowerPC
Mailing List itcl-request@tclk.com with a subject of: subscribe

Other Book References Tcl/Tk Tools

[incr Tcl] is to Tcl what C++ is to Tcl, right down to the pun for the name. It extends the base Tcl language with support for:

- Namespaces.
- Class definition with:
  - Public, private, and protected class methods.
  - Public, private, and protected data.
  - Inheritance.
  - Constructors.
  - Destructors.
- Variables attached to a class rather than a class instance.

The namespace commands were first introduced into Tcl by [incr Tcl]. The [incr Tcl] namespace command has same basic format as the namespace command in Tcl 8.0. One difference is that [incr Tcl] allows you to define items in a namespace to be completely private. A pure Tcl script can always access items in a Tcl namespace using the complete name of the item.
