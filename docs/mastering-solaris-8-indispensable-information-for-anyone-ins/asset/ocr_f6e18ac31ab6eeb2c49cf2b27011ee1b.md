+   * Response headers
+   * The entity headers
+   * The entity body

The response status consists of a single line with the following syntax:
`HTTP/<version><status_code> <reason_phrase>`

`<version>` corresponds to the version of HTTP that the server is using to respond.
`<status_code>` is a number from 100 to 599, which indicates whether the request was successful or not. The response codes are categorized in Table 14.1.

**TABLE 14.1: RESPONSE CODES**

| Range | Explanation |
| :--- | :--- |
| 100~199 | Information from the server |
| 200~299 | Successful requests |
| 300~399 | Redirected requests |
| 400~499 | Incomplete or failed requests |
| 500~599 | Server errors |

The two most common status codes are 301 and 302. Status code 301 indicates that a URL has been relocated permanently, and status code 302 indicates that a URL has been relocated temporarily. Clients that receive a status code from 300 through 399 make a new request to the new URL automatically. The error codes 400 through 499 and 500 through 599 indicate client or server errors, respectively. The client has requested a page that it does not have permission to access or the page does not exist or has been removed.

`<reason_phrase>` is a readable description of the status code and is usually OK to indicate a successful request. ERR indicates a failed request.

The general headers, as in the request, include information such as the type of connection and the time the server began its task. The response header contains information about the server. It may also indicate which HTTP methods the general headers and response headers support.

The entity header and body are returned by the server if the client's request was successful. The entity header contains information about the type of data that is being returned, including the size of the requested document and the time the file was last modified.