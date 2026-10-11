performance if they are not available when User Processes need them. The Shared Servers themselves are only one component of the Shared Server architecture.

![](bbox=[0.13, 0.18, 0.24, 0.26])

On Windows 2000 systems all user Server Processes execute within the OS threads associated with the **oracle.exe** executable, not as discrete OS processes as they do on Unix systems. Therefore, the **Shared Server** feature does not provide the same scalability improvements on Windows 2000 systems that it does on Unix systems.

# Shared Server Architecture

When you need a taxicab, you have to first telephone the taxicab company and notify them that you need a ride. The taxicab company will pass your request to the taxicab dispatcher, who places your name on the list of persons wanting a cab. The taxicab dispatcher then assigns your request to a particular cab, which will eventually come to your address and pick you up, and take you to your destination. The **Shared Server** architecture has several components that perform similar functions. The components of the **Shared Server** architecture are:

+   - User Processes
+   - Oracle Net Listener Process
+   - Dispatcher Processes
+   - Request Queue
+   - Shared Server processes
+   - Response Queue

Each of these components is discussed in the following sections.

**User Process** Each application user, whether they initiate their database connection via a client-based executable or via a middle tier application server, creates a **User Process** that manages their connection to the Oracle server machine.

**Oracle Net Listener** The Oracle Net Listener listens for incoming client requests for data or DML activity. When a request is detected, the listener assigns the request to the least busy Dispatcher Process.