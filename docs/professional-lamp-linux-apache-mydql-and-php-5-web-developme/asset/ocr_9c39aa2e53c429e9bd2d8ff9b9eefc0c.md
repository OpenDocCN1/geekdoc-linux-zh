# Chapter 7

When the “evil” username value is substituted into the original query, the effective set of commands would look like this:

```
SELECT * FROM Users WHERE username='';
DELETE FROM Users;
SELECT 'Ow3d' AS username FROM Users WHERE ''=''
```

When the data sent to the SQL server is not escaped as in this example, any number of bad things can happen. Imagine the damage if the middle command was a DROP DATABASE or GRANT command — not a good situation. This example is a rather simplified case of what can happen during a SQL injection attack, but it should give you a taste of what kind of damage it can do to your data and system integrity.

Like many of the common problems plaguing PHP scripts, SQL injection is somewhat preventable with a little planning and thorough code hygiene practices. If configured with `magic_quotes_gpc` set to on, PHP has got your back with regards to escaping “dangerous” characters in your form data. When `magic_quotes_gpc` is enabled, PHP automatically escapes any escape characters, such as apostrophes, before you can even touch them in your script. Unfortunately, this behavior is applied to all GET, POST, and cookie variables, regardless of whether they’re going to be used in a SQL statement or not — and most of the time it can be a little annoying.

To make sure your data is escaped only when you need it to be, turn off `magic_quotes_gpc` in `php.ini`, and use `addslashes()` on all data that is being passed to MySQL. The `addslashes()` function will automatically escape any dangerous characters so your input will not choke MySQL — both on SQL injection attacks, and legitimate data with special characters, such as last names with apostrophes.

As a second line of defense, make sure the user you access the database with in PHP has only the minimum amount of privileges needed to keep the application running. In the previous SQL injection attack, the deletion of all the user records would have actually failed — when the user was set up at the beginning of the chapter, only SELECT rights were granted.

A relative to SQL injection attacks, filesystem execution attacks, should be treated in a similar manner. Any uncleared input data that becomes part of a call to `system()` or `exec()` should be considered suspect, as they can easily be a handful of malicious system commands chained together in a similar way to SQL injection attacks.

# Cross-Site Scripting

While SQL injection and `register_global` abuse deal primarily with the usage of dirty input data, there is another kind of attack that relies on the uncleanness of the dynamic output instead—cross-site scripting.

Commonly abbreviated XSS, cross-site scripting is the exploiting of unfiltered dynamic output, where the attacker has the ability to add or change the page’s generated markup. Most commonly, this means the addition of a small bit of JavaScript to the output data of a page, which then does something sinister, such as trick another user into revealing their login credentials or credit card information, or possibly divulging cookie or session information for immediate account compromise.