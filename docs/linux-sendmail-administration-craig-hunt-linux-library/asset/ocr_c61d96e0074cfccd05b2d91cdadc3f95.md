# Processing Input Mail Headers

In addition to defining your rulesets, you can call a ruleset from a header definition to check the format of the headers your system receives. Sometimes spammers use malformed headers that indicate the mail is spam. Assume you're getting spammed by someone who forgets to create a valid-looking Message-Id: header. You could use code like that shown in Listing 11.5.

# Listing 11.5 Checking Header Contents

```
LOCAL_RULESETS
Message-Id: $>check_MID_header

Scheck_MID_header
R$+ @ $\$OK
R$* $: 550: Invalid Header
```

The LOCAL_RULESETS section contains an H command for the sendmail.cf file. Unlike the commands we saw in Chapter 7, "sendmail.cf File," this doesn't contain a header format. Instead, it uses the $ syntax to call a ruleset to process the header. This example calls ruleset check_mid_header because that is the name of the new ruleset defined in Listing 11.5.

The Scheck_MID_header command is the first line of ruleset check_MID_header. This ruleset is essentially identical to the one described in the previous example. It checks to make sure that the Message-Id contains both a unique identifier and a hostname in the format. All other formats are rejected as errors.

I don't recommend that you use either of these rewrite rule examples because I don't use them. I simply created them to illustrate how these rules are used. Frankly, I don't develop rules to fight spam. First, rewrite rules can be complex and difficult to develop. I don't want them to be worse than the disease. Second, the format of spam mail is constantly changing. The rule I write today may be useless tomorrow. I think it is better to rely on the MAPS RBL, the access database, and the ability of the user's mailer to filter.

# Filtering Out Spam from the Mailer

Despite your efforts, spam and unwanted mail will get to your users. In part this is because you can't block all of the spam and in part this is not all unwanted e-mail is spam. Sometimes a user doesn't want to look at some legitimate e-mail simply because of personal preference. In this case, the mail needs to be filtered by the user's mail