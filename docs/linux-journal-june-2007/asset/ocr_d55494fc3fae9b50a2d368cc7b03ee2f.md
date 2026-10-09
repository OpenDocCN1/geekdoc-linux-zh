# FEATURE Validate an E-Mail Address with PHP

```
Listing 9. A Complete E-mail Validation Function
```php
/**
 * Validate an email address.
 * Provide email address (raw input)
 * Returns true if the email address has the email
 * address format and the domain exists.
 */
function validEmail($email)
{
    $isValid = true;
    $atIndex = strpos($email, "@");
    if (is_bool($atIndex) && !$atIndex)
    {
        $isValid = false;
    }
    else
    {
        $domain = substr($email, $atIndex+1);
        $local = substr($email, 0, $atIndex);
        $localLen = strlen($local);
        $domainLen = strlen($domain);
        if ($localLen < 1 || $localLen > 64)
        {
            // local part length exceeded
            $isValid = false;
        }
        else if ($domainLen < 1 || $domainLen > 255)
        {
            // domain part length exceeded
            $isValid = false;
        }
        else if ($local[0] == '.' || $local[$localLen-1] == '.')
        {
            // local part starts or ends with '.'
            $isValid = false;
        }
        else if (preg_match('/\\\\./', $local))
        {
            // local part has two consecutive dots
            $isValid = false;
        }
        else if (!preg_match('/[A-Za-z0-9!#$%&'*+\/.^_`{|}~--]+$/', $domain))
        {
            // character not valid in domain part
            $isValid = false;
        }
        else if (preg_match('/\\\\./', $domain))
        {
            // domain part has two consecutive dots
            $isValid = false;
        }
        else if (!preg_match('/^([A-Za-z0-9!#$%&'*+\/.^_`{|}~--]+)\\.',
                            str_replace("\\", "", $local)))
        {
            // character not valid in local part unless
            // local part is quoted
            if (!preg_match('/["'](["'])+["']+$/',
                            str_replace("\\", "", $local)))
            {
                $isValid = false;
            }
        }
        if ($isValid && !(checkdnsrr($domain,"MX") ||
                          checkdnsrr($domain,"A")))
        {
            // domain not found in DNS
            $isValid = false;
        }
    }
    return $isValid;
}
```
```

The local part is a wrap. The code now checks all local part requirements. Checking the domain will complete the e-mail validation. The code could check all of the labels in the domain separately, as does the whiskey-loving code shown in Listing 2, but, as hinted earlier, the solution presented here allows the DNS check to do most of the domain validation work.

Listing 7 makes a cursory check to ensure only valid characters in the domain part, with no repeated dots. It goes on to make DNS lookups for MX and A records. It makes the check for the A record only if the MX record check fails. The code in Listing 4 verified the length of the domain name.

So, is it good? You decide. But, it would be nice to test the logic to ensure that it at least is correct. Listing 8 contains a series of e-mail address test cases that any e-mail validation should pass. Be sure to run the test to see the valid and rejected e-mail addresses, the double-escaping \ (\) inside the PHP strings tends to obfuscate the addresses. You’re challenged to subject your favorite e-mail validation code to this test. Be assured that the code in Listing 9 does pass!

Listing 9 contains a complete function for validating an e-mail address. It isn’t as concise as many—it certainly isn’t a one-liner. But, it is straightforward to read and comprehend, and it correctly accepts and rejects e-mail addresses that many other published functions incorrectly reject and accept. The function orders the validation tests roughly according to increasing cost. In particular, the more complex regular expression and, certainly, the DNS lookup, both come last.

Spread the word! There is some danger that common usage and widespread sloppy coding will establish a de facto standard for e-mail addresses that is more restrictive than the recorded formal standard. If you want to fool the spambots, adopt an e-mail format like [^\^|D@*^G@^cartron.com. Unfortunately, you might find some legitimate e-commerce sites as well. Which do you suppose will adapt more quickly?

> Douglas Lowel is a software engineer with IBM Rational, author of The XSL Formatting Objects Developer’s Handbook published by Sams, and Web site editor for ia452.org.