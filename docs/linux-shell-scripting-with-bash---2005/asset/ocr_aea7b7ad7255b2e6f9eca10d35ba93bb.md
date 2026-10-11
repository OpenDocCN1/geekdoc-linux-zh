```
printf "&nbsp;<br />"
printf "<i>If the problem persists, contact tech support.</i></p>"
rm -f "$ERRORS"
fi

# Write HTML Trailer

printf "&nbsp;<br /></h6>"
printf "Host %s - Script %s - Time " "$HOSTNAME" "$SCRIPT"
date
printf "</h6>"
printf "</body>"
printf "</html>\n"

exit 0
```

Run `form.cgi` with the form in Listing 16.5 to see a list of variables from the form and the decoded values.

Suppose you had a form to send a message to the tech support department.

# Listing 16.5 form.html

```
<html>
<head>
<title>Form Test</title>
</head>
<body>
<h1>Ask Tech Support Question</h1>
<form action="http://localhost/cgi-bin/form.cgi">
<input type="submit" name="submit" value="Send Question">
<input type="textarea" name="message" value="" maxlength="80">
<input type="text" name="name" value="" maxlen="80">
</form>
</body>
</html>
```

When the form is submitted to form.cgi, the decode function reports:

```
Var 1 submit is 'Send Question'
Var 2 message is 'When will the email system upgrade occur?'
`
Var 3 name is 'Alice Q. Walters`
End of CGI variables
```