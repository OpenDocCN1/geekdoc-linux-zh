These fields represent the following information:

+   - **Host name:** This is the hostname or IP address of the client requesting a document.
+   - **Client identity:** If the client is running identd and the IdentityCheck directive is enabled, the identity information provided by the client is placed in this field.
+   - **Username:** If the requested URL required basic HTTP authentication, the username used to authenticate appears in this field.
+   - **Date:** The date and time of the request in the form `[dd/mm/yyyy:hh:mm:ss zzzz]`. For instance, a typical date might be `[30/Jan/2000:04:23:35 -0800]`. The zzzz portion of the field (in this case `-0800`) is the time zone’s offset from GMT.
+   - **Request:** This field contains the exact text of the client’s request header surrounded by double quotes. This field makes it possible to determine which document was requested. A typical entry is similar to `GET /manual/mod/core.html HTTP/1.1`.
+   - **Status:** This field contains a three-digit code specifying the HTTP status code returned by Apache. HTTP status codes are outlined in Table 23.5.
+   - **Bytes:** This field contains the number of bytes transferred.

Where a field does not contain any information (as can be the case with the client identity and username fields), the field will simply contain a dash (-). The status field will contain one of the status codes outlined in Table 23.5.

**TABLE 23-5  HTTP 1.1 STATUS CODES**

| Status Code | Name | Description |
|---|---|---|
| 100 | Continue | The server is ready to receive the rest of the request from the client. |
| 101 | Switching Protocols | The server is willing to switch to an application protocol specified by the client in an Upgrade header. |
| 200 | OK | The server has processed a request successfully and is returning it to the client. |
| 201 | Created | The server has created a new URL based on a `Location` header. |
| 202 | Accepted | The server has accepted a request and will process it. |
| 203 | Non-Authoritative Information | The information in the response header was copied from another server. |
| 204 | No Content | The server has successfully processed a request but no new information need be displayed by the client. |
| 205 | Reset Content | The client should reset the currently displayed document. |
| 206 | Partial Content | The server has successfully processed a partial GET request. |