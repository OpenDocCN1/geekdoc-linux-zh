```
The following parameters are optional:

C=/page/uri    to define a different page to gather initial cookies from
(h|H)=My-Hdr\: foo to send a user defined HTTP header with each request
`USER[64]^ and `PASS[64]^ can also be put into these headers!

Note: 'h' will add the user-defined header at the end
regardless it's already being sent by Hydra or not.
'H' will replace the value of that header if it exists, by the
one supplied by the user, or add the header at the end
Note that if you are going to put colons (: ) in your headers you should escape them wi
All colons that are not option separators should be escaped (see the examples above a
You can specify a header without escaping the colons, but that way you will not be ab
in the header value itself, as they will be interpreted by hydra as option separators
.
.
```

*Listing 610 - Additional information about the http-form-post module*

From this output, we determine that we need to provide a number of arguments that will require us to perform some application discovery. First, we need the IP address and the URL of the webpage containing the web form on our Windows client. The IP address will be provided as the first argument to hydra.

Next, we must understand the web form we want to brute force by inspecting the HTML code of the web page in question (located at /form/login.html).

Figure 294 shows the code of the target web form after right-clicking the page and selecting **View Page Source** from the context menu:

![](bbox=[0.23, 0.49, 0.77, 0.72])

The above form, part of the /form/login.html page, indicates that the POST request is handled by /form/frontpage.php, which is the URL we will feed to Hydra. The syntax displayed in Listing 610 requires the form parameters, which in this case are user and pass. Since we are attacking the admin user login with a wordlist, the combined argument to Hydra becomes /form/frontpage.php:user=admin&pass=^PASS^, with ^PASS^ acting as a placeholder for our wordlist file entries.