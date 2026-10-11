PwnKit: Privilege Escalation: Bypasses: PwnKit: Privilege: Escalation

![](bbox=[0.12, 0.085, 0.88, 0.54])

Figure 241: Identifying the exact browser version through the http://developers.whatismybrowser.com user agent database

Notice that the User Agent string implicitly tells us that Microsoft Edge 41 is running on the 32-bit version of Windows 10. For 64-bit versions of Windows, the string would have otherwise contained some information regarding the 64-bit architecture as shown below:

```
Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537 Edge/16.16299
```

Listing 382 - The complete User Agent string for the same version of Microsoft Edge on a 64-bit version of Windows

We managed to gather the information we were after, but the JavaScript code from Listing 380 displays data to the victim rather than to the attacker. This is obviously not very useful so we need to find a way to transfer the extracted information to our attacking web server.

A few lines of Ajax³⁸ code should do the trick. Listing 383 shows a modified version of the previously used fingerprint web page. In this code, we use the XMLHttpRequest JavaScript API to interact with the attacking web server via a POST request. The POST request is issued against the same server where the malicious web page is stored, therefore the URL used in the xmlhttp.open method does not specify an IP address.

³⁸ [Wikipedia, 2019], https://en.wikipedia.org/wiki/Ajax_(programming)