
Note the title `Greetings` that was passed onto the method. The two `p()` methods produce the following:

```html
<p>Hello Carol Godsave.</p>
<p>Thanks for coming to our Web site.</p>
```

And finally, the `end_html()` method produces the following:

```html
</body></html>
```

which ends the HTML document.

Careful readers will notice that we have violated the first CGI programming style guide, which states that we should separate contents and logic. This little script has HTML inside the script, which makes it harder to modify for a non-programmer. But this script was meant as a mere exercise. In the following section, I look at a useful, production-grade script that conforms to the style guidelines.

## Creating a basic Web form processor

Most common CGI scripts are used as the back-end of a Web form. Virtually, every Web site has a Web form that takes user input and stores it in a file or database. In the following section, I present a very customizable CGI script that can work with virtually any single-page Web form.

## Features of a basic Web form processing CGI script

Say that your Web site will have one or more Web forms that need to collect data from Web visitors to store in files or databases. One CGI script-based solution, which has the following features:

- **Supports multiple Web forms:** A single script will work for multiple, single-page Web forms. A single-page Web form asks all its questions in a page. There are times when you will be asked to build a multi-page Web form, which falls into the category of custom form-processing applications. Such form-processing applications usually use custom business logic to display multiple forms and are beyond the scope of this book. My personal recommendation, based on years of Web development, is to avoid multipage Web forms because people often become discouraged when asked to answer a long series of questions. Also, when designing a single-page Web form, do not ask too many questions. Keeping the data collection to a minimum is good practice when generating new leads. Experience tells me that new prospects and leads are turned off by a huge form or by a multi-page form session, and often decide to forget about doing business with the site all together.
- **Centralized configuration for all Web forms:** The script uses a configuration file, which supports multiple Web forms. Each Web form configuration can be separately stored in this standard configuration file, which means you can centralize your form configuration information — a very good thing for a busy system administrator.
- **Comma Separated Value (CSV) files for data storage:** The script allows you to save data in CSV files. Each form can have its own CSV file. You can also specify the order of fields and which fields you want to store.

To make learning about this CGI script simpler and more realistic, I will assume that you have a User Registration Web form called `register.html` as shown in Listing 12-3.

### Listing 12-3: register.html

```html
<html>

<body bgcolor="white">

<font face="Arial" size=+1>User Registration Form</font><br>
<p>
<form action="/cgi-bin/formwizard.pl" method="POST">

<table border=0
    cellpadding=3
    cellspacing=0
    bgcolor="#000000">
<tr>
<td>

<table border=0
    cellpadding=5
    cellspacing=5
    bgcolor="#abcdef">

<tr>
<td> Name </td>
<td> <input name="name" type=text size=30 maxsize=50> </td>
</tr>

<tr>
<td> Email </td>
<td> <input name="email" type=text size=30 maxsize=50> </td>
</tr>

<tr>
<td> Zipcode</td>
<td> <input name="zipcode" type=text size=30 maxsize=50> </td>
</tr>

<tr>
<td> Can we send you junk mail?</td>
<td>
<input type=radio name="opt-in" value="yes">Yes, Please!
<input type=radio name="opt-in" value="no">No, Never!
</td>
</tr>

<tr>
<td align=center> <input type-submit value="Register Me"</td>
<td align=center> <input type=reset> </td>
</tr>

</table>
</td>
</tr>
</table>
</form>
<p>
</html>
```

This Web form looks as shown in Figure 12-5.

![](img/e11fcbd2818a3495ac70085e5d8d1c26_381_0.png)

**Figure 12-5:** The register.html form in a Web browser.

This example Web form has four data fields: name, email, zipcode and an opt-in question. This is a typical user registration form except that most sites will not ask the opt-in question as (honestly) posed in this form. When a user fills out this form, the data has to be stored in a file, and the user is displayed a thank you message or taken to a new page. For example, if the above form is filled out, it can show a thank you message as shown in Figure 12-6.

![](img/e11fcbd2818a3495ac70085e5d8d1c26_382_0.png)

**Figure 12-6:** Thank you message for filling out *register.html*.

## Developing a Web form processor CGI script in Perl

Now let's develop a CGI script in Perl that enables you to create a Web form-processing solution as shown in the example in the last section. Figure 12-7 shows the flow diagram of such a CGI solution.

When this script is called as the form action in *register.html*, as shown here:

```html
<form action="/cgi-bin/formwizard.pl" method="POST">
```

This script performs the following tasks:

1. Loads all external standard (i.e. part of standard Perl distribution) and other CPAN modules
2. Loads the central configuration file, which should have a configuration specific to the Web form that posted data to it.
3. Creates a CGI object that enables it to retrieve posted data and to access other information supplied by the Web server.
4. Determines if the Web form that activated the script has a configuration in the central configuration file. If it does not, then it simply displays an error message stating that this form cannot be processed by this script. If it does have a configuration, it starts form processing.
5. As the first processing step, the script validates the user data. This step involves checking data validity based on the requirements stated in the configuration file and performing sanity checks on data fields supplied by the user.
6. If the validation step returns no errors, the data is stored in a data file. On the other hand, if the data validation step fails because of user error(s), then an error message specific to the type of error(s) is displayed and processing is aborted.
7. If the previous step is successful, the script displays a thank you message or redirects the user to another URL and terminates.

![](img/e11fcbd2818a3495ac70085e5d8d1c26_382_1.png)

The *formwizard.pl* script is included in the CDROM.

![](img/e11fcbd2818a3495ac70085e5d8d1c26_383_0.png)

**Figure 12-7:** CGI Web form-processing diagram.

## Looking at formwizard.pl

The *formwizard.pl* script implements this flow diagram. In the *formwizard.ini* configuration file, the *register.html* fields have these restrictions:

- The *name* field is required and set to be from 3 to 50 characters in length. The field value must be composed of characters ranging from a- to z and the period. If the field value passes the length and pattern tests, it is stored as a string in which each word starts with a capital letter.
- The *email* field is also required and it must be between 6 and 100 characters. Acceptable characters for an e-mail address are a to z, 0 to 9, dash (-), underscore (_), period, and the AT (@) symbol. The *email* pattern test is applied to the value of this field and if all (length, character set, and pattern) tests are passed by the value, it is stored in lowercase format.
- The zipcode field is treated as an optional number field, which must pass the us_zipcode pattern test if the user enters a value. The us_zipcode pattern test simply checks whether the entered number is either a five-digit number or a five-digit number with a four-digit number to form zip codes such as 95825-1234. The only characters allowed are 0 to 9 and the dash.
- Finally, the opt-in field is considered a required text field that can only have a value of 'yes' or 'no'.

## Listing 12-4: formwizard.ini Configuration File

```ini
# --------------------------------------------------------
#
# Web Form Configuration for *** register.html *** form
#
# --------------------------------------------------------

[register.html]
template_dir = /www/asb2/ch12/forms/register

# --------------------------------------------------------
# After the form is processed, the script must acknowledge to
# the user that the system received the data. This is done
# using a "Thank You" (called thankyou hereafter)
# message.
#
# Set the name of the thankyou template here
# --------------------------------------------------------
thankyou_template = thanks.html

#
# --------------------------------------------------------
# If you wish to redirect the user to another URL,
# set the URL here. Do not set this to any URL
# if you wish to show the thankyou message instead
#
# If the URL is set, it is always used instead of
# showing the thankyou message.
# --------------------------------------------------------
thankyou_redirect_url = /asb2/ch12/forms/feedback.html

#
# --------------------------------------------------------
# The script will either show the thankyou message or
# redirect the user to another URL.
# If you wish to send data to the redirect URL via GET method
# set this to 'yes'; otherwise, set it to 'no'.
# --------------------------------------------------------
send_data_on_redirect = no

#
# --------------------------------------------------------
# Having a specific list of form fields
# ensures that we only use what we need.
# We will ignore any additional field(s)
# --------------------------------------------------------
```
