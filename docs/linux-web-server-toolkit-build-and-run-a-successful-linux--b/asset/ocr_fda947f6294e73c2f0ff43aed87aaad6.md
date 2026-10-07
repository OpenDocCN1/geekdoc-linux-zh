# Chapter 17: Using Server APIs

# 413

| Module | Purpose |
| --- | --- |
| mod_digest | Provides MD5 authentication to the server. |
| mod_example | An example module for demonstrating the Apache API (for Apache 1.2 or later). |
| mod_expires | Allows the Expires: header to be used with resources (relative to caching of documents). |
| mod_log_agent | Allows for logging of User Agents (the browser used by the person requesting a document). |
| mod_log_referer | Allows for logging of which HTML document provided the link to the requested document (when this information is provided by a browser). |
| mod_negotiation | Controls negotiation of content for things like compression, graphics type, and so forth. |
| mod_rewrite | Provides URL-to-filename mapping using UNIX regular expressions. |
| mod_speling | Used to automatically correct typos in URLs (Apache 1.3 or later). |
| mod_unique_id | Generates a unique identifier for every browser request, which you can use for stateful system, logging, and so forth (Apache 1.3 or later). |

# # Introduction to the Netscape API

The FastTrack server for OpenLinux has a comprehensive programming interface from which most of the server's functionality is derived. In fact, the FastTrack server uses this API to build the regular functions for the directives used in magnus.conf (the server configuration file) and obj.conf (the object configuration file). Using the application programming interface (API), you can create-plugins to insert into the directives in server configuration files.

Because the same API is used for your own applications and for the core of the FastTrack server, when you become familiar with the API, you also learn more how the server works. This means you can override the server functionality, add to it, or customize your own functions. Examples include creating functions that use a different type of database for access control (including working with an Oracle or NetWare NDS database on your OpenLinux system).

The FastTrack server can also use JavaScript or Java, JNI, and JavaScript. The API provides a lower-level interface for CGI, Java, and JavaScript. The API is a set of ANSI C functions and header files that use a common object model to interface with your own code.