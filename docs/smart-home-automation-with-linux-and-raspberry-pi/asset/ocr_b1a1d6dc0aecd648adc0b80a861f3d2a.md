Add any per-file control with a change to `.htaccess` thusly:

```
```apache
<Files private_file.php>
    require valid-user
</Files>
```
```

Note, however, that although you don’t need to restart Apache for these changes to take place (because you’re not changing apache2.conf or its partners), you do need to ensure the following appears within those directory directives that use this authentication system:

```
```apache
AllowOverride AuthConfig
```
```

This is because most examples will default the previous line to the following, which does not support the feature:

```
```apache
AllowOverride None
```
```

You can also create groups of users by adding lines to the `.htpasswd` file:

```
```apache
FamilyGroup: mum dad sister
HouseOwnersGroup: mum dad
```
```

And you can amend the requirements line `.htaccess` to this:

```
```apache
Require group HouseOwnersGroup
```
```

When accessing these authorized-only web pages, you will be presented with a dialog box requesting your username and password. This naturally makes the page appear more difficult to bookmark. In fact, isn’t the HTTP specification allows both of these to be passed as part of the URL.

[http://myusername:mypassword@myprivatesite.homelinux.org](http://myusername:mypassword@myprivatesite.homelinux.org)

Although this is a security flaw, it must be remembered that the authorization credentials are already passed in plain text, so it does not open any new holes; it merely lowers the barrier to entry for script kiddies. Provided that the bookmark isn’t stored on any publicly accessible machine, you are no worse off.

> > **Note**  Be aware that some media players will display the full URL (including login credentials) when streaming music from such a site.

A much-improved form of security is through Secure Sockets Layer (SSL). This is where two sites (the client and server) will communicate only once they have established that a proven secure connection exists by the exchange of certificates. These certificates prove that the server claiming to be `minervahome.net`, for example, really is the server located at `minervahome.net`. This certificate of authenticity, as it were, is issued by a higher authority who’s reliability you can trust. And this authority is verified by an even higher authority, and so on. At the top of this hierarchy are companies such as VeriSign, whose entire worth is based on the fact they can never be confused with anyone else. Acquiring these certificates of trust costs money and is generally reserved for businesses, although home users are not explicitly excluded. However, you can always get around this requirement by generating a certificate that you sign yourself. This doesn’t provide the full security package, but it provides secure access to your data that can’t be seen by anyone else on the network.