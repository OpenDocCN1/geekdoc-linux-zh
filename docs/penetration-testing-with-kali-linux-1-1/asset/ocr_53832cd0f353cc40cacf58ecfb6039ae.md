```
Listening on http://0.0.0.0:8000
Document root is /home/kali
Press Ctrl-C to quit.
```

Listing 306 - Using PHP to run an HTTP server on port 8000

We can also launch an HTTP server with a Ruby “one liner”. The command requires several flags including `–run` to load `un.rb`, which contains replacements for common Unix commands, `–e httpd` to run the HTTP server, `.` to serve content from the current directory, and `–p 9000` to set the TCP port.

```
kali@kali:~$ ruby –run –e httpd , –p 9000
[2019-08-28 12:44:14] INFO WEBrick 1.4.2
[2019-08-28 12:44:14] INFO ruby 2.5.5 (2019-03-15) [x86_64-linux-gnu]
[2019-08-28 12:44:14] INFO WEBrick::HTTPServer#start: pid=1367 port=9000
```

Listing 307 - Using Ruby to run an HTTP server on port 9000

We can also use `busybox`, “the Swiss Army Knife of Embedded Linux”, to run an HTTP server with `httpd` as the function, `–f` to run interactively, and `–p 10000` to run on TCP port 10000:

```
kali@kali:~$ busybox httpd –f –p 10000
```

Listing 308 - Using BusyBox to run an HTTP server on port 10000

To stop any of these servers, we can simply hit **Ctrl C**.

Next, let’s discuss PHP wrappers.

# 9.4.4.9 PHP Wrappers

PHP provides several protocol wrappers ${}^{279}$ that we can use to exploit directory traversal and local file inclusion vulnerabilities. These filters give us additional flexibility when attempting to inject PHP code via LFI vulnerabilities.

We can use the ${}^{280}$ wrapper to embed inline data as part of the URL with plaintext or base64 ${}^{281}$ encoded data. This wrapper provides us with an alternative payload when we cannot poison a local file with PHP code.

Let’s take a closer look at how to use the data wrapper. We start it with “data:” followed by the type data. In this case, we’ll use “text/plain” for plaintext. We follow that with a comma to mark the start of the contents, in this case “hello world”. When we put it all together, we get “data:text/plain,hello world”.

We already know the menu page is vulnerable to LFI attacks. If we submit a payload using a data wrapper, the application should treat it the same as a regular file and include it in the page. Let’s check if this works by submitting the following URL and checking the results:

```
http://10.11.0.22/menu.php?file=data:text/plain,hello world
```

Listing 309 - A test payload using the data wrapper

${}^{279}$ (The PHP Group, 2019), https://www.php.net/manual/en.wrappers.php
${}^{280}$ (The PHP Group, 2019), https://www.php.net/manual/en/wrappers.data.php
${}^{281}$ (Wikipedia, 2019), https://en.wikipedia.org/wiki/Base64