# Chapter 13. Extensions and Packages

```
set fsearch [formBUTTON f "" "Search for Name" \
"SearchName"]
set fexit [formBUTTON f "" "EXIT" "formDIE f; dbClose db; \\exit"]
formEND f $fsearch
```

# Script Results

![](bbox=[0.228, 0.255, 0.906, 0.388])

# 13.5 Sybtcl and Oracl

Language - C

Primary Site - http://www.neosoft.com

Contact - tpoindex@nyx.net, Tom Pointerdex

Tcl Revision Supported - Tcl: 7.3-8.0 Tk: 3.6-8.0

Supported Platforms - Unix, Windows NT, Windows 95

Sybtcl and Oracle are Tcl interfaces to the Sybase and Oracle database libraries. These packages allow you to use Tcl to write programs that interact with a database server.

In general, these two packages follow the same style of interaction with the Tcl interpreter and the database libraries. This consistency makes it easy to convert an application from one brand of database server to another.

The packages maintain the flavor of the C library for their respective servers. Hence, there are some optimized database access techniques that are available in one extension that are not available in the other.

542