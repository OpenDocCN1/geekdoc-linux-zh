# OffSec vulnerabilities are mostly used for gathering information.

Directory traversal is mostly used for gathering information. As mentioned before, if we can access files containing sensitive information, passwords or keys, it may lead to system access.

In most cases, the web server is in the context of a dedicated user such as data. These users usually have limited access permissions on the system. However, users and administrators often intentionally set file permissions to be very permissive or even world-readable. Sometimes this occurs due to time constraints in deployment or less-mature security programs. This means we should always check for the exposure of SSH keys and their access permissions.

SSH keys are usually located in the home directory of a user as .ssh folder. Fortunately for us, /etc/passwd shows the home directory paths of all users, as shown in Figure 126. The output of /etc/passwd shows a user called offsec. Let's specify a relative path for the "page" parameter to display the contents of the user's private key.

```
http://mountaindesserts.com/meteor/index.php?page=../../../../../../home/offs/ssh/id_rsa
```

Listing 135 - Entry URL of Directory Traversal

Let's copy the url from 135 into the address bar of our browser.

![](bbox=[0.125, 0.43, 0.875, 0.58])

Figure 127 shows that we successfully retrieved the private key for user offsec. The output, we might notice that its formatting is a bit messy.

During web assessments, we should understand that as soon as we have identified a possible vulnerability, such as the "page" parameter in this case, we should not rely on a browser for testing. Browsers often try to parse for user friendliness. When performing web testing, we should mainly use tools such as Burp, cURL or a programming language of our choice.

387 (PortSwiger, 2022), https://portswigger.net/burp
388 (Curl, 2022), https://curl.se/