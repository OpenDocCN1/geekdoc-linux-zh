| Field | Information |
| :--- | :--- |
| special-action-flag | Characters that indicate when special action was taken: |
| | C indicates the file was compressed; |
| | U indicates the file was uncompressed; T indicates the file was |
| | tar_d;- indicates that no action was taken. |
| direction | Direction of the transfer: o indicates an outgoing transfer; |
| | i indicates an incoming transfer. |
| access-mode | The method that the user logged in: |
| | a indicates an anonymous login; |
| | g indicates the guest account; |
| | r indicates a real user |
| username | The local user name. |
| service-name | The name of the service invoked, which is usually ftp. |
| authentication-method | The method of authentication: |
| | 0 indicates no authentication; |
| | 1 indicates RFC931 authentication. |
| authenticated-user-id | The user ID returned from the authentication method. A * is used |
| | if the user ID is not available. |
| completion-status | Character that specifies if the transfer was completed: |
| | c indicates a completed transfer; |
| | i indicates an incomplete transfer. |

# Using FTP server utilities

You can use several tools to manage the FTP server and monitor its function. These tools are as follows:

+   - ftpshut
+   - ftpwho
+   - ftpcount

# The ftpshut command

The `ftpshut` command is used to gracefully shut down the FTP server at a given time while providing warning to users. The format is as follows, and Table 16-7 shows the parameters:

```
ftpshut  [  -V  ] [ -l min] [ -d min] time [ warning-message... ]
```