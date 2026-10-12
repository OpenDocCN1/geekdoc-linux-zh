# Authenticaton

You can encode and un-encode base-64 data using the Linux program **mimencode**. Like many UNIX programs, this will either read the standard input direct from your keyboard (type Ctrl-C to terminate), or you can use the echo program to pipe a string to it. Examples of both are shown below. Decoding is very similar, but you give the encoded data as input and give the “-u” un-encode option to **mimencode**. The example we’ve used is from the headers in Module 14.17.

```
```
alice% mimencode
leopard:blooms
b6GVcG9sZDpibG9vbXM=
^C
alice%

alice% echo leopard:blooms | mimencode
b6GVcG9sZDpibG9vbXM=
```
```

# SSL

The SSL specification and related documents:

+   - http://www.netscape.com/eng/ssl3/

For an introduction to symmetric and public-key (asymmetric) cryptography, see

+   - http://www.garykessler.net/library/crypto.html Gary Kessler’s *An Overview of Cryptography*

# Character-based browsers – retrieving Web pages automatically

+   - http://lynx.browser.org/ – the Lynx text browser

+   - http://www.gnu.org/software/wget/wget.html – GNU Wget, a free software package for retrieving files using HTTP, HTTPS, and FTP

# Appendices

Appendix 17: HTTP/1.1 server response codes