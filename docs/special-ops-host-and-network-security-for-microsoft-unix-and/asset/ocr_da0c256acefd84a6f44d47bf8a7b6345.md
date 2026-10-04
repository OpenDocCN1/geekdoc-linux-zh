# Chapter 13 + Attacking and Defending Oracle

package exposes procedures that can be called directly, but also has functions that are called internally from within another package. The PL/SQL module for Apache extends the functionality of a Web server, enabling the Web server to execute these stored PL/SQL packages in the database. The best way to imagine the PL/SQL module is a gateway into an Oracle Database Server over the Web using stored procedures. By default, all requests to the Web server leading with /pls are sent to the PL/SQL module to be dispatched. The client request URI will contain the name of a Database Access Descriptor (DAD), the name of the PL/SQL package in the database server and the procedure being accessed. Any parameters that there are to passed to the procedure are in the query string:

```
http://oracleserver/pls/bookstore/books.search?name=Special+Ops
```

This URL has a DAD of bookstore, a PL/SQL package called books, and a procedure search, which takes a parameter name, the name of the book to search for. The DAD describes a section in the wdbsvr.app file that describes how Apache is to connect to the database server and contains details such as the supplied, UserID and password to authenticate with. If no credentials are supplied, the request would result in the Web client prompted for credentials. On connecting to the database server, the database will load the books package and execute the search procedure; the search results would be passed back to the Web server, which would then pass them on to the requesting client.

# Format String Vulnerability in the PL/SQL Module

If an attacker makes a request to the Web server for a non-existent package and/or procedure, the database server will reply with a message:

```
XXXX: PROCEDURE DOES NOT EXIST
```

The problem is this message is then passed as the format string to the _sprintf() function. Needless to say, making a request to the Web server with an attacker-supplied format string may be possible to gain control of the Apache server. For example the URL http://oraclewebserver/pls/%25x%25x%25x%25n%25n%25n.foo will crash the Web server. Because this is coming from the heap and not the stack, creating a special format string may be possible to overwrite program control structures such as saved return addresses or function pointers.

![](bbox=[0.066, 0.943, 0.296, 0.971])