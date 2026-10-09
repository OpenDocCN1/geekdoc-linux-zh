✦ Centralized configuration for all Web forms: The script uses a configuration file, which supports multiple Web forms. Each Web form configuration can be separately stored in this standard configuration file, which means you can centralize your form configuration information — a very good thing for a busy system administrator.

✦ Comma Separated Value (CSV) files for data storage: The script allows you to save data in CSV files. Each form can have its own CSV file. You can also specify the order of fields and which fields you want to store.

To make learning about this CGI script simpler and more realistic, I will assume that you have a User Registration Web form called `register.html` as shown in Listing 12-3.

# **Listing 12-3: register.html**

```
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
```