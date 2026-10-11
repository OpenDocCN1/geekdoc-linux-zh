If a file is created with the extension of .hta instead of .html, Internet Explorer will automatically interpret it as a HTML Application and offer the ability to execute it using the mshta.exe program.

The purpose of HTML Applications is to allow arbitrary execution of applications directly from Internet Explorer, rather than downloading and manually running an executable. Since this clashes with the security boundaries in Internet Explorer, an HTML Application is always executed outside of the security context of the browser by the Microsoft-signed binary mshta.exe. If the user allows this to happen, an attacker can execute arbitrary code with that user’s permissions, avoiding the security restrictions normally imposed by Internet Explorer.

While this attack vector only works against Internet Explorer and to some extent Microsoft Edge, it is still useful since many corporations rely on Internet Explorer as their main browser. Moreover, this vector leverage features directly built into Windows operating systems and, more importantly, it is compatible with less secure Microsoft legacy web technologies such as ActiveX.341

# 13.2.1 Exploring HTML Applications

Similar to an HTML page, a typical HTML Application includes html, body, and script tags followed by JavaScript or VBScript code. However, since the HTML Application is executed outside the browser we are free to use legacy and dangerous features that are often blocked within the browser.

In this example, we will leverage ActiveXObjects,342 which can potentially (and dangerously) provide access to underlying operating system commands. This can be achieved through the Windows Script Host functionality or WScript343 and in particular the Windows Script Host Shell object.344

Once we instantiate a Windows Script Host Shell object, we can invoke its run method345 in order to launch an application on the target client machine.

Let’s create a simple proof-of-concept HTML Application to launch a command prompt:

```
```
<html>
<body>

<script>
    var c='cmd.exe'
    new ActiveXObject('WScript.Shell').Run(c);
</script>

</body>
</html>
```
```

+   - 341 (Wikipedia, 2019), https://en.wikipedia.org/wiki/ActiveX
+   - 342 (Microsoft, 2017), https://developer.mozilla.org/en-US/docs/Web/JavaScript/Microsoft_Extensions/ActiveXObject
+   - 343 (Microsoft, 2015), https://docs.microsoft.com/en-us/previous-versions/windows/internet-explorer/ie-developer/windows-scripting/atsyd31(v=vs.84)
+   - 344 (Microsoft, 2015), https://docs.microsoft.com/en-us/previous-versions/windows/internet-explorer/ie-developer/windows-scripting/aew9yb99(v=vs.84)
+   - 345 (Adersoft, 2019), http://www.vbsedit.com/html/6f28899c-d653-4555-8a59-49640be32ea.asp