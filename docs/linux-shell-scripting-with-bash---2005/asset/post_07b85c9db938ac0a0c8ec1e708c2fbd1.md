
- `SERVER_PORT`—The TCP/IP port used to connect to the Web server
- `SERVER_PROTOCOL`—Version of HTTP used by the server
- `SERVER_SOFTWARE`—Description of the Web server

## Processing Forms

The HTML equivalent of environment variables is the form. Each form contains a set of variables. For example, the form input tag

```html
<input type='hidden' name="user" value="bmith">
```

is the HTML equivalent of

```bash
declare user="bmith"
```

Other nonhidden input tags represent variables whose values can be changed by the user through items on the form. Such items include buttons, menus, and text boxes. In all these cases, the choices made by the user are saved as new values of the variable before the form is sent to a CGI script.

Because the CGI script doesn't receive a copy of the Web page, how then does it know the values of the input tags? There are two methods. The older **GET** method stores the HTML variables in an environment variable called `QUERY_STRING`. Consider the following form.

```html
<html>
<head>
<title>Form Test</title>
</head>
<body>
<form action="http://localhost/cgi-bin/form.cgi">
<input type="hidden" name="user" value="bmith">
<input type="submit" name="submit" value="Click Me!">
</form>
</body>
</html>
```

The query string contains the names and values of the two variables.

`user=bmith&submit=Click+Me%21`

One of the reasons forms are difficult to work with is that the information is encoded. The standard form encoding (x-www-form-urlencoded) converts spaces to plus signs and non-alphanumeric characters to ASCII hexadecimal numbers with leading percent signs. In this case, the exclamation point is converted to hexadecimal 21.

The **POST** method writes the variables to standard input, eliminating the risk of a buffer overflow in the Web server if the list of variables becomes very long. It also keeps the variables off of the Web page URL. If a script reads the variables in a while loop, the final line is not executed in the while because the line doesn't end in a line feed.

```bash
while read LINE; do
    echo "$LINE"
done
echo "$LINE"
```

This displays the same encoded information that appears in QUERY_STRING when the GET method is used.

`user=smith&submit=Click+Me%21`

The form.cgi script shown in Listing 16.4 decodes and displays the form variables.

### Listing 16.4 form.cgi

```bash
#!/bin/bash

# form.cgi - decode and display all variables in a form

shopt -s -o nounset

# DECODE: decode all variables in $1 and display them

function decode {
    declare VARIABLES="$1"         # the list of variables to process
    declare VAR                     # variable to decode
    declare NAME                    # variable name
    declare VALUE                   # value of variable
    declare LAST                    # last decoded variable
    declare -i CNT=1                # running total of variables processed
    declare PART1                   # part before % hex code
    declare PART2                   # part after a % hex code
    declare TMP                     
    declare REMAINING               # remaining variables to process
    declare HEX                     # ASCII code as hexadecimal
    declare OCT                     # ASCII code as octal

    # Replace '+' with ' '
    VARIABLES="${VARIABLES//+/ }"

    # Hex code replacement

    while true; do
        LAST="$VAR"                 # remember last variable
        VAR="${VARIABLES%%&*}"     # extract next variable
        REMAINING="${VARIABLES*&}"  # variables left to process
        NAME="${VAR%*=}"           # variable's name is before =
        VALUE="${VAR#*=}"          # variable's encoded value is after =

        # Process any hex values

        while true; do
            PART1="${VALUE%%\%*}"          # value before last %
            if [ "$PART1" = "$VALUE" ]; then # same as whole value?
                break                              # then no % left
            fi
            TMP="${VALUE#*\%}"            # value after last %
            HEXA="${TMP:0:2}"                # extract two digit hex code
            PART2="${TMP:2}"                  # value after the hex code
            VALUE="$PART1"$(printf "\\x$HEXA")"$PART2" # combine, replacing hex code
        done
        printf "Var %d %s is `%s`\n" "$CNT" "$NAME" "$VALUE" # display variable
        if [ "$REMAINING" = "$VARIABLES" ]; then # remaining same as last?
            printf "%s\n" "<br />"           # all variables done
            printf "%s\n" "End of CGI variables<br />" # display end message
            break
        fi
        VARIABLES="$REMAINING"               # do remaining variables
        CNT=CNT+1                              # increment count
    done
} # end of decode
readonly -f decode
declare -t decode

# Declarations

declare -rx SCRIPT=${0##*/}
declare GATEWAY_INTERFACE
if [ ! -z "$GATEWAY_INTERFACE" ]; then
    printf "%s\n" "$SCRIPT: this script should be run by a web browser" >&2
    exit 192
fi

declare -rx ERRORS=`mktemp /tmp/env.errors.XXXXXX`
if [ ! -z "$ERRORS" ]; then
    ERRORS=`/tmp/env.errors.XXXXXX`
    printf "%s\n" "mktemp failed" 2> "$ERRORS"
fi
declare QUERY_STRING               # ensure QUERY_STRING exists
declare REQUEST_METHOD               # ensure REQUEST_METHOD exists

# Write Response Header

printf "Content-type: text/html\r\n"
printf "\r\n"

# Write HTML Header

printf "<html>"
printf "<head>"
printf "<title>$SCRIPT results</title>"
printf "</head>"
printf "<body>"
printf "<h1>$SCRIPT results</h1>"

# For POST, read the data into QUERY_STRING
# Otherwise, variables are already in QUERY_STRING

if [ "$REQUEST_METHOD" = "POST" ]; then
    while read LINE; do
        QUERY_STRING="$QUERY_STRING$LINE"
    done
    QUERY_STRING="$QUERY_STRING$LINE"
fi

# Generate Web Page to Return

# Display original, encoded variables

printf "Processing: $QUERY_STRING<br />"

printf "<pre>"

decode "$QUERY_STRING" 2> "$ERRORS"

printf "</pre>"

# Display any errors

if test -s "$ERRORS"; then
    printf "%s\n" "$ERRORS"
    printf "<table border=\"1\" summary=\"errorlist\">"
    printf "<tr bgcolor=\"White\"><td>"
    printf "<font color=\"black\" size=\"3\"><b>"
    printf "<p><b>Error(s)</b><br />"
    printf "<pre>"
    cat "$ERRORS"
    printf "</pre></font></td></tr></table>"
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

### Listing 16.5 form.html

```html
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
Var 3 name is 'Alice Q. Walters'
End of CGI variables
```

The script works for both GET and POST forms. Figure 16.1 shows a picture of the tech support example.

![](img/7da864b222941ec315ee1c456ff472dd_314_0.png)

Figure 16.1 The Ask Tech Support form.

## Basic Web Page Stripping (lynx)

Vast amounts of information are available in Web pages on the Internet. Headlines can be pulled from news sites. Prices can be stripped from competitor's sites. Much of this information is publicly available and accessible from shell scripts.

The easiest way to access this information is through lynx, the text Web browser available on most Linux distributions. lynx has two modes for retrieving data for script processing. The -source switch returns the HTML source code for the Web page just as if you used the View Source option on a graphical Web browser.

```bash
$ lynx -source http://www.pegaoffa.ca | head -10
<?xml version="1.0"?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" 
        "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" 
<head>

<meta name="generator" content="HTML Tidy, see www.w3.org" />
<meta http-equiv="Content-Type" 
      content="text/html; charset=iso-8859-1" />
<meta name="description" content="Linux Software Solutions" />
<meta name="keywords"
```
