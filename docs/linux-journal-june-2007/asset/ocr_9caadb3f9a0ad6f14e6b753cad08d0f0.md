# Listing 8. Test the e-mail validation function.

```
<?php
require("validateMail.php"); // your favorite here

function testEmail($email)
{
    echo $email;
    $pass = validateMail($email);
    if ($pass) {
        echo " is valid.\n";
    } else {
        echo " is not valid.\n";
    }
    return $pass;
}

$pass = true;
echo "All of these should succeed:\n";
$pass &= testEmail("dcloiou.1bm.com");
$pass &= testEmail("abc\@Wdef@example.com");
$pass &= testEmail("abc\\\@example.com");
$pass &= testEmail("Fred B\Blogs@example.com");
$pass &= testEmail("Joe.\\B10w@example.com");
$pass &= testEmail("^"AbcWdef"@example.com");
$pass &= testEmail("\"Fred Blogs"@example.com");
$pass &= testEmail("customer/department=shipping@example.com");
$pass &= testEmail("$A123456@example.com");
$pass &= testEmail("!def!xyz$abc@example.com");

$pass &= testEmail(".someename@example.com");
$pass &= testEmail("user+mailbox@example.com");
$pass &= testEmail("peter.piper@example.com");
$pass &= testEmail(""Doug\" \\ ""Ace"" \\ ""L""L"@example.com");
$pass &= testEmail(""Doug\" \\ ""Ace"" \\ ""L""@example.com");
echo "\nAll of these should fail:\n";
$pass &= !testEmail("abc\@Wdef@example.com");
$pass &= !testEmail("abc\\@Wdef@example.com");
$pass &= !testEmail("abc\\@example.com");
$pass &= !testEmail("@example.com");
$pass &= !testEmail("doug@"));
$pass &= !testEmail(""""@example.com"));
$pass &= !testEmail("o@o\@example.com"));
$pass &= !testEmail(".dot@example.com");
$pass &= !testEmail("dot_.dot@example.com");
$pass &= !testEmail("two..dot@example.com");
$pass &= !testEmail("""Doug\" \\ ""Ace"" \\ ""L""@example.com");
$pass &= !testEmail("""Doug"" \\ ""Ace"" \\ ""L""@example.com");
$pass &= testEmail("hello world@example.com");
$pass &= !testEmail("gatsby@f.s.c.ot.f.i.tz.g.m.r.1.d.");
echo "\nThe email validation ";
if ($pass) {
    echo "passes all tests.\n";
} else {
    echo "is deficient.\n";
}
?>
```

Now, the local part has one of two forms. It may have a begin and end quote with no unescaped embedded quotes. The local part, Doug \"Ace\" L. is an example. The second form for the local part, (+.+), where + stands for a whole slew of allowable characters. The second form is more common than the first; so, check for that first. Look for the quoted form after failing the unquoted form.

Characters quoting using the back slash (\) pose a problem. This form allows doubling the back-slash character to get a back-slash character in the interpreted result (\). This means we need to check for an odd number of back-slash characters quoting a non-back-slash character. We need to allow \\\\ and reject \\\\\\.

It is possible to write a regular expression that finds an odd number of backslashes before a non-backslash character. It is possible, but not pretty. The appeal is further reduced by the fact that the backslash character is an escape character in PHP strings and an escape character in regular expressions. We need to write four back-slash characters in the PHP string representing the regular expression to show the regular expression interpreter a single back slash. A more appealing solution is simply to strip all pairs of back-slash characters from the test string before checking it with the regular expression. The str_replace function fits the bill. Listing 5 shows a test for the content of the local part.

The regular expression in the outer test looks for a sequence of allowable or escaped characters. Failing that, the inner test looks for a sequence of escaped quote characters or any other character within a pair of quotes.

If you are validating an e-mail address entered as POST data, which is likely, you have to be careful about input that contains back-slash (\), single-quote (') or double-quote ("") (\). PHP may or may not escape those characters with an extra back-slash character wherever they occur in POST data. The name for this behavior is magic_quotes_gpc, where gpc stands for get, post, cookie. You can stop the magic code via the function, get_magic_quotes_gpc(), and strip the added slashes on an affirmative response. You also can ensure that the PHPini file disables this 'feature'. Two other settings to watch for are magic_quotes_runtime and magic_quotes_sybase.

The two regular expressions in Listing 5 are appealing because they are relatively easy to comprehend and don't require repetition of the allowable character group ([A-Za-z0-9!#$%&'*+\-/=?^_`{|}~-.]). Here's a test for you. Why does the character group require two back-slash characters before the forward slash and one back-slash character before the single quote?

One deficiency of the outer test of Listing 5 is that it passes local part strings that include dots anywhere in the string. Requirement number two states that dots can't start or end the local part, and they can't appear together two or more times. We could address this by expanding the outer regular expression into form (+a+), where a is [(\\[A-Za-z0-9!#$%&'*+\-/=?^_`{|}~-.])\. We could, but that leads to a long, hard-to-read, repetitive expression that's difficult to believe in. It's clearer to add the simple checks shown in Listing 6.