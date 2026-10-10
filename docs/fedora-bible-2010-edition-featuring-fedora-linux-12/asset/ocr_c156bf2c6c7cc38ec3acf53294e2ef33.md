| Token | Description |
| :--- | :--- |
| `$u` | If access-control rules require username and password authentication, this represents the username supplied by the client. |
| `$U` | The URL requested by the client. |
| `$v` | The canonical name of the server according to the Domain Name System (DNS). |
| `$V` | The canonical name of the server handling the request according to the UseCanonicalName directive. |
| `$X` | The connection status after the response is finished. A status of X means the connection was closed before the response was completed, + means the connection may be kept open (alive) after the response, and - means the connection will be closed after the response is sent to the client. |

The *common* format includes the client host's name or IP address, the username as reported by the ident daemon and the server's authentication method (if applicable), the local time at which the request was made, the actual HTTP request, the server response code, and the number of bytes transferred. This format is a de facto standard among Web servers (and lately even among FTP servers).

For the purpose of connection tracking, the *referer* format stores the URL (from the same site or an external server) that linked to the document just delivered (relative to the *ServerRoot*). For example, if the page `http://www.example.com/corp/about_us.html` contained a link to your home page at `http://www.mybox.com/linxguy/bio.html`, when a client accessed that link, the referer log on www.mybox.com would look like:

```
http://www.example.com/corp/about_us.html -> /linxguy/bio.html
```

This information can be used to determine which path each client took to reach your site.

The *agent* format stores the contents of the User-agent: HTTP header for each incoming connection. This field typically indicates the browser name and version, the language, and the operating system or architecture on which the browser was run. Accessing an Apache server from a Firefox browser on a Linux system running on a PC produces the following entry:

```
Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.9.1.3) Gecko/20090911
Fedora/3.5.3-1.fc12 Firefox/3.5.3
```

The *combined* format concatenates all the information from the other three log file formats into one line. This format is useful for storing all connection-related log entries in one centralized file. The *combined* format, which is connected out by default, can be enabled (by removing the # character) to log the actual number of bytes received (`%I`) and sent (`%O`), provided the *mod_logio* module is loaded.