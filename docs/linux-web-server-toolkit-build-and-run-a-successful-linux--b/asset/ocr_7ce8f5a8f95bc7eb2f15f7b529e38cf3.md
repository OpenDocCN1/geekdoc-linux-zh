# Linux Web Server Toolkit

3. See if the user included a query or needs to be sent only the empty form
(used more for GET queries).

4. Process the data sent (and gathered in step 2).

5. Send appropriate HTML headers back to the browser by writing to Standard
Output as if writing to the screen, followed by a blank line that marks the
beginning of the HTML page.

6. Send the appropriate HTML page back to the browser; the page is often
created by the script but can also be pulled from one of several existing
HTML files on the server.

This section presents some script fragments in Perl that do several of the tasks
just outlined. Step 4 depends completely on what your script intends to accom-
plish. The other steps have a common form that is illustrated here. Although thou-\ands of example Perl scripts are available on the Web, if you're not familiar with
Perl, creating programs using shell scripts is an easier way to begin responding to
forms on your Web server.

# CHECK WHICH METHOD WAS USED

Most scripts are designed to use either POST or GET, depending on their purpose\and the form or HTML page that calls them. The following script fragment example
checks to see if the correct method was used (GET in this case); if it wasn't, an error
message is returned to the browser:

```
if ($ENV{REQUEST_METHOD} ne GET ) {
  &error_page( Page was not accessed with GET operation. );
```

Note use the $ENV array in Perl to access an environment variable (many
are created by the Web server specifically for scripts to access), and the use of
sub subroutine, called send_error_page here, to send the headers and HTML data of a
basic document. A sample subroutine is shown in the next section.

# REMOVE SPECIAL CHARACTERS FROM A GET QUERY STRING

Because the query string sent with a GET request uses special characters (+, %,
hexadecimal), a script must convert the special characters to normal text before the
query can be processed. The following Perl script fragment converts those charac-
ters; it is written as a subroutine that your scripts can call before dividing the query
string into separate name-value pairs:

```
sub remove_escapes {
local($line) = @;
# you can also try $line=$QUERY_STRING
```