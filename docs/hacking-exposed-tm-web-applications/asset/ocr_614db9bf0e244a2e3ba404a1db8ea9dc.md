# Chapter 4: Surveying the Application

Now we have the name of the form—gs. We know that it uses GET instead of POST and it calls a script called "search" in the Web root directory. Going back to our search for helper files, the next few files we look for are search.inc, search.js, gs.js, and gs.js. A lucky guess never hurts. Remember to download the HTML source of the /search file, if possible.

Next, find out what fields the form contains. Source-sifting is required at this stage, but we'll compromise with grep to make things easy:

```
[root@meddle]# getit.sh www.victim.com /index.html | \\
> grep -i "input type"
www.victim.com [192.168.23.26] 80 (http)
<input type="text" name="name" size="10" maxlength="15">
<input type="password" name="password" size="10" maxlength="15">
<input type="hidden" name="vote" value="websites">
<input type="submit" name="Submit" value="Login">
```

This form shows three items: a login field, a password field, and the submit button with the text, "Login." Both the username and password must be 15 characters or less (or the application would like to believe). The HTML reveals a fourth field called "name." An application may use hidden fields for several purposes, most of which seriously inhibit the site's security. Session handling, user identification, passwords, items costs, and other sensitive information tend to be in hidden fields. We know you're chomping at it to actually try some input validation, but be patient. We have to finish gathering all we can about the site.

If you're trying to create a brute-force script to perform FORM logins, you'll want to enumerate all of the password fields (you might have to use the \\" characters):

```
[root@meddle]# getit.sh www.victim.com /index.html | \\
> grep -i="password"
www.victim.com [192.168.23.26] 80 (http)
<input type="password" name="passwd" size="10" maxlength="15">
```

Tricky programmers might not use the input type or have the words "pass-word" or "passwd" in the form. You can search for a different string, although its hit rate might be lower. New Web browsers use an autocomplete function that saves users from entering the same information every time they visit a site. For example, the browser might save the user's address. Every time the browser detects an address field, that is, searches for "address", it will fill the user's information automatically. However, the autocomplete function is usually set to "off" for password fields:

```
[root@meddle]# getit.sh www.victim.com /login.html | \\
> grep -i autocomplete
www.victim.com [192.168.106.34] 80 (http)
<input type="text" name="val2" size="12" autocomplete="off">
```

![](bbox=[0.913, 0.903, 0.959, 0.936])