# 9

# Getting Control—Regular Expression Metacharacters

![](bbox=[0.61, 0.07, 0.84, 0.36])

By the end of this chapter, you will be able to unravel and use the following regular expressions:

```
die unless (/^*@[\^".]*,\.*[a-z]({2},$)/);
```

```
$money = s/(?<=\$)(?= (\d\d\d)+(?1\d))//g
```

# 9.1 The RegExLib.com Library

Before getting deep into the weeds, let's take a look at the *regexlib.com* Web site. This Web site allows you to search for a pattern and will show you a list of regular expression solutions and a rating on how well each one performs its pattern-matching task. Although the Web site may not be 100 percent Perlish in the way it handles regexes, it is certainly a good research tool when you're trying to get some clues on how to write your own. The following is the opening statement found at the home page of *RegExLib.com* (also shown in Figure 9.1).

> Welcome to **RegExLib.com**, the Internet's first Regular Expression Library.
> 
> Currently we have indexed **3800** expressions from **2172** contributors around the world. We hope you'll find this site useful and come back whenever you need help writing an expression, you're looking for an expression for a particular task, or are ready to contribute new expressions you've just figured out. Thanks!