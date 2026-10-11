# Concurrent Client Servers

All of the servers presented in this text so far have processed one client's request in total before accepting a connection to the next client. This design is effective and simple for servers that reply swiftly. However, if the processing takes a long time, or there are periods of inactivity, then this will prevent other clients from being serviced without lengthy delays. Because servers are usually required to service as many clients as possible, with a minimum of delay, a fundamental design change is needed at the server end of the connection.

In this chapter you will learn how to use the following:

+   The fork(2) function in order to handle multiple client connections
+   The wait(2) and waitpid(2) functions
+   The select(2) function for handling multiple client connections

Mastering these concepts will permit you to write professional-grade servers, which can service large numbers of clients at once.