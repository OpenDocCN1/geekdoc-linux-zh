```
Common Name (eg, your name or your server's hostname)
[ ]:www. **industrialpressinc.com**
Email Address [ ]: **webmaster@industrialpressinc.com**
```

The preceding generation process places all files in the proper place. All you need to do is restart your Web server and add https instead of http in front of your URL. Don't forget: you'll get a certificate validation message from your Web browser, which you can safely ignore.

# Exporting Encryption Technology

For many years, the United States government treated encryption technology like munitions. As a result, anyone wanting to export encryption technology had to get an export license from the Commerce Department. This applied not only to encryption software developed within the United States, but also to software obtained from other countries and then re-exported to another country (or even to the same country you got it from). Thus, if you installed encryption technology on your Linux system and then transported it out of the country, you were violating federal law! Furthermore, if you e-mailed encryption software to a friend in another country or let him or her download it from your server, you violated the law.

In January 2000, the U.S. export laws relating to encryption software were relaxed considerably. However, often the U.S. Commerce Department's Bureau of Export Administration requires a review of encryption products before they can be exported. U.S. companies are also still not allowed to export encryption technology to countries classified as supporting terrorism.

# Restarting your Web server

By now you've probably noticed that your Web server requires you to enter your certificate password every time it is started. This is to prevent someone from breaking into your server and stealing your private key. Should this happen, you are safe in the knowledge that the private key is a jumbled mess. The cracker will not be able to make use of it. Without such protection, a cracker could get your private key and easily masquerade as you, appearing to be legitimate in all cases.

If you just cannot stand having to enter a password every time your Web server starts, and are willing to accept the increased risk, you can remove the password encryption on your private key. Simply do the following:

```
# cd /etc/pki/tls/private
# /usr/bin/openssl rsa -in localhost.key -out localhost.key
```

# Troubleshooting your certificates

The following tips should help if you are having problems with your SSL certificate: