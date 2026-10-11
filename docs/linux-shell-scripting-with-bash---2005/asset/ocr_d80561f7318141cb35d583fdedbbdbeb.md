# # CGI Environment Variables

CGI programs have additional environment variables assigned by the Web server. Different Web servers include different variables. Here is a list of some common variables:

+   - AUTH_TYPE—Authorization type if pages are password protected
+   - CONTENT_LENGTH—Number of bytes being written to standard input (for POST forms)
+   - CONTENT_TYPE—The form's content type
+   - DOCUMENT_ROOT—The root directory of the Web server's document tree
+   - GATEWAY_INTERFACE—The version of the CGI standard being used by the Web server
+   - HTTP_ACCEPT—Types of data acceptable to the browser (for example, `text/html`)
+   - HTTP_ACCEPT_CHARSET—Character set requested by the Web browser
+   - HTTP_ACCEPT_ENCODING—Compression methods allowed by the Web browser (for example, `gzip`)
+   - HTTP_ACCEPT_LANGUAGE—Language requested by the Web browser (for example, `en for English`)
+   - HTTP_USER_AGENT—The browser used by the user
+   - HTTP_HOST—The URL's hostname
+   - HTTP_REFERER—The Web page executing this CGI program
+   - PATH_INFO—Extra information included in the URL
+   - PATH_TRANSLATED—PATH_INFO, as a file/directory under the root of the document tree
+   - QUERY_STRING—for GET forms, the variables on the form
+   - REMOTE_ADDR—IP of the user's computer
+   - REMOTE_HOST—Hostname of the user's computer
+   - REMOTE_USER—Username used when accessing password-protected pages
+   - REQUEST_METHOD—Usually `GET` or `POST`
+   - SCRIPT_NAME—Pathname of the script being executed
+   - SCRIPT_FILENAME—The absolute pathname of the script being executed
+   - SERVER_ADDR—IP address of the Web server
+   - SERVER_ADMIN—Email address to email messages to the person in charge of the Web server
+   - SERVER_NAME—Domain name of the Web server