# # C API Reference

T his appendix describes the C language application programming interface for the MySQL client library. The API consists of a set of functions for communicating with MySQL servers and accessing databases, and a set of data types used by those functions. The client library functions may be classified into the following categories:

+   - Routines for initializing and terminating the client library
+   - Connection management routines to establish and terminate connections to the server
+   - Error-reporting routines to get error codes and messages
+   - Construction and execution routines to construct SQL statements and send them to the server
+   - Result set processing routines to handle results from statements that return data
+   - Information routines that provide information about the client, server, protocol version, and the current connection
+   - Transaction control routines
+   - Routines for processing multiple result sets
+   - Routines for server-side prepared statements
+   - Administrative routines for controlling server operation
+   - Thread routines for writing threaded clients
+   - Routines for generating debugging information

Unless otherwise indicated, the data types and functions listed here have been present in the client library at least as early as MySQL 5.0.0. Changes made since then are so noted.

The examples in this appendix are only brief code fragments. For complete client programs and instructions for writing them, see Chapter 7, “Writing MySQL Programs Using C.”