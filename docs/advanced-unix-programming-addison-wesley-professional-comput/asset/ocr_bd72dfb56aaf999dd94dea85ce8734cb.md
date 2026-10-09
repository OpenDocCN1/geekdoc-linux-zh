The server determines whether the document exists and if the client can have access to it. If not, it responds with a status line like
`HTTP/1.1 404 Not Found\r\n`
which is followed by an HTML document that explains the error. (We’ll get to how documents are sent in a moment.)

If the file can be sent, the status line is like
`HTTP/1.1 200 OK\r\n`

Each document, whether HTML text, a JPEG, or whatever, is preceded by a header that describes it, which has this general form (in our examples, anyway):

```
```
Server: servername\r\n
Content-Length: length\r\n
Content-Type: type\r\n\r\n
```
```

The *servername* can be anything; we’ll use “AUP-ws” for our servers. The *length* is the length of the document in bytes so the client knows how much to read. That way the connection can be left open, since the client doesn’t need an EOF to tell it to stop reading. The *type* is a so-called MIME (Multipurpose Internet Mail Extensions) type, only two of which we care about: “text/html” and “image/jpeg.” (There are dozens more.) After the header comes the document, exactly as it exists on the server’s file system.

# ### 8.4.3 SSI Web Browser

Here’s a simple Web browser called *minibr*. As with the earlier examples, it can retrieve HTML; however, it doesn’t know how to interpret the tags for a nice screen display, so it just dumps everything to the standard output:

```
```c
int main(void)
{
    char url[100], s[500], *path = "", *p;
    SSI *ssip;
    int fd;
    ssize_t nread;

    while (true) {
        printf("URL: ");
        if (fgets(url, sizeof(url), stdin) == NULL)
            break;
        if ((p = strchr(url, '\n')) != NULL)
            *p = '\0';
```
```