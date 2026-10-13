Note that all usernames must be lowercase characters for this to work. If you have usernames that are alphanumeric, you have to use a different regular expression.

# Using ScriptAliasMatch

Using the ScriptAliasMatch directive also enables you to support CGI program directories for each user. For example,

```
ScriptAliasMatch ~([a-z]+)/ \
cgi-bin/(.*)/home/$1/public_html/cgi-bin/$2
```

matches username to $1, where $1 is equal to ~([a-z]+), and matches everything followed by /cgi-bin/ to $2, where $2 is equal to (.*). Then, it uses $1 and $2 to create the actual location of the CGI program directory. For example:

```
http://www.yourcompany.com/~joe/ \
cgi-bin/feedback.cgi?book=dummies&author=kabir
```

In this example, ~([a-z]+) will map one or more lowercase characters following the tilde mark (~) to $1. In other words, the pair of parentheses enables you to capture everything between the tilde (~) and the trailing forward slash (/) after the username. So, $1 is set to kabir and (?) maps everything following the cgi-bin/ and the parentheses pair in this regular expression, and enables you to put everything in $2. Thus, $2 is set to search.cgi?book=dummies&author=kabir.

Now, Apache can create the physical path of the CGI program directory using the following:

```
/home/$1/public_html/cgi-bin/$2
```

This regular expression results in the following path for the previous example: