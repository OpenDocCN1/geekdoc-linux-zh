A suite of functions has been packaged with Zope for safe use in Python
scripts. To access them, place the following import statement at the top of your
Python script:

```
import Products.PythonScripts.standard
```

This import statement gives you access to the following functions:

| Function | Description | Example | Result |
| --- | --- | --- | --- |
| html_quote(value) | Replaces characters significant to HTML with their corresponding HTML entities. | html_quote('>>Click Here') | &gt;Click&lt; |
| url_quote(value) | Escapes characters in URLs. | url_quote('spaced out') | spaced%20out |
| url_quote_plus (value) | like url_quote, but substitutes + spaces. Used for CGI variable values. | url_quote('spaced out') | spaced+out |
| newline_to_br (value) | Replaces newline characters in a string with <br> HTML tags. | newline_to_br(""Home on the range"") | Home<br>on the<br>range |
| structured_text (value) | Renders a string containing structured text into HTML. | structured_text('*This_*is* *structured text,*') | <u><em>is&lt;/</em>><b>structured text</b></b>. |
| whole_dollars (value) | Formats a number as a whole dollar amount. | whole_dollars(4.5) | $4 |
| dollars_and_cents (value) | Formats a number as dollars and cents. | dollars_and_cents(4.5) | $4.50 |
| thousand_commas (value) | Formats a number with commas at thousands place. | thousand_commas(1000000) | 1,000,000 |

#  14.6 Calling Python Scripts from DTML

Python scripts can be called with any DTML tag that uses the name or expr attributes. Normally, you will use dtml-var or dtml-call to execute a Python script: dtml-var if the script returns a value to be inserted, and dtml-call if no insertion is desired or no value is returned by the script. If the Python script has no parameters in its parameter list you can call it using name="..." notation as shown here:

```
<dtml-var name="pythonScript">
```