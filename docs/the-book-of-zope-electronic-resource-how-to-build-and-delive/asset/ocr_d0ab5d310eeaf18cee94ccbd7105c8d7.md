| Name | Description |
| --- | --- |
| SERVER_SOFTWARE | The name and version of the information server software that responds to the query, using the format Name/Version. |
| SERVER_NAME | The hostname, the DNS Alias, or the IP address of the server as it appears in the URL. |
| GATEWAY_INTERFACE | The version of a CGI specification that the server is using. Format is CGI/Version. |
| SERVER_PROTOCOL | The name and version of the infirmation protocol from which the query originates. Format is Protocol/Version. |
| SERVER_PORT | The port number to which the query was sent. |
| REQUEST_METHOD | The method that was used to create the query. For HTTP: GET, HEAD, POST, and so on. |
| PATH_INFO | The part of the queried URL (without the start string) that follows the name of the Zone installation or module published by ZPublisher. |
| PATH_TRANSLATED | The server returns a translated version of PATH_INFO, which takes the path and maps it from a virtual to a physical one. |
| SCRIPT_NAME | Returns a virtual path to the executed script; used with self-referring URLs. |
| QUERY_STRING | The information that follows the ? in the URL, which refers to this script. This is the query information. |
| REMOTE_HOST | Returns the name of the host that created the query. If the server does not have this information, it should call REMOTE_ADDR and leave REMOTE_HOST blank. |
| REMOTE_ADDR | Returns the IP address of the remote host that placed the request. |
| AUTH_TYPE | If the server supports user authentication and the script is protected, this log-specific authentication method is used to confirm the validity of the user. |
| REMOTE_USER | If the server supports user authentication and the script is protected, the user is authenticated under this name. |
| REMOTE_IDENT | If the HTTP Server supports RFC 931 identification, this variable is set to the username obtained from the server. Restrict use of this variable to login only. |
| CONTENT_TYPE | In the case of queries that have information attached, for example HTTP POST and PUT, this is the content type for the data. |
| CONTENT_LENGTH | Returns the length of the specified content as entered by the client. |