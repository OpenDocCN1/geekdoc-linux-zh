
this lesson uses grep as its example, familiarize yourself with this format so that you can draw from it as we continue to use it throughout the chapter.

> What Is This, Another Root Directory? I am Confused
Do not get overwhelmed by the amount of characters and their meanings all at once. This is what I have found to be one of the biggest hurdles when learning Unix as a beginner—trying to remember the countless commands, their options, dealing with case sensitivity, and now with a whole slew of characters that have meanings and functionality.

In the case with REs, other programs sometimes require the regular expression to be set with a / on either side of it; this is not the case with grep. Be aware that you may have syntax issues so consult your local man pages and online documentation (or your systems administrator) if you are in a jam.

## Using . and *

Let's look at building a new file to practice using regular expressions. In this example, we will use grep in conjunction with the . and * REs. Since REs will specify a method of matching, I will attempt to drive home the concept of REs with a search through a simple text file that you can create with the vi editor or emacs.

Make a file that has the current information within it:

```
Rob's Test File
Rob Shimonski
"aka Unix junkie"
2006
2005
2004
2003
2002
2001
2000
1999
1999
```

Once you have finished, save and name the file robtest.txt.

This file will serve as the data we will search to learn how to use REs. In this example, we will use the period (.), which can be used to match any character as a single unit, and the asterisk (*), which you can use to match any number of occurrences of a pattern or portion of a pattern. To make this concept easier to understand, let's look at an example of both when using REs with grep to search the robtest.txt file for specific information.

```
> grep "Shimon..." robtest.txt
Rob Shimonski
```

In this example, we saw the use of grep, which was used against the robtest.txt file to search for my name "Shimonksi." It was able to do, even though I left the last three letters "ski" off, and intentionally put in three periods that Unix could come back to me with what it found in the robtest.txt file as a match. This can be used in multiple ways, such as the following:

```
> grep "Shi..n.ki" robtest.txt
Rob Shimonski
```

```
> grep "S..mo..ki" robtest.txt
Rob Shimonski
```

As you can see, it really doesn't matter what you specify, you just need to specify what is a known exactly as shown in the file so Unix can find for it. Unix will attempt to find what it thinks you are looking for, so don't be surprised if you don't narrow your search down and get thousands of answers from Unix. The period (.) is primarily used to narrow down your search. In cases where you don't really know, and don't mind the possibility of a long and timely search, you can use the asterisk (*).

If you were able to do the first example, then you are definitely able to handle this one because all you are doing is applying a slightly different concept here:

```
> grep "S.*i" robtest.txt
Rob Shimonski
```

With last names like mine, using a wildcard is sometimes your only hope.

> Okay, Don’t Set Me Off Now! There are more ways to use grep and REs. This chapter can only cover so much, so it’s my intent to interest you and then look on your own.

Use \ to set off a special character. Some characters are used by the shell, so they must be escaped by using \. You might want to use this in front of characters that might be special characters as well. In most cases, it doesn't hurt to use \ if you aren't sure. For example, the shell usually expects to put double quotes (\") around strings with them. It uses the double quotes to group the words in the string. If you need to search through your file for lines containing double quotes, you cannot grep for " instead, use the following command:
> grep "\"" robtest.txt
aka Unix "junkie"

Using the \ in front of the double quotes tells the shell to not attempt to interpret the double quotes normally as a surrounding character, but to instead simply pass it to the grep command for processing.

## Using [] and ^

In this section, we will learn more about REs, particularly when using and negating ranges using the [] and ^ characters.

## Regular Expressions 163

You've noticed that the robtest.txt file you created and have been using the years 1899 through 1999 inside of it. We will use grep again in conjunction with REs to match the years that only fall in the 2000 range. To do this, you can specify a range using REs as: [<starting point--ending point]]. The starting and ending points can be numbers or ranges within the alphabet.

For example, type the following:

```
grep "1-[8-9][0-9]*" robtest.txt
1999
1899
```

This example lets Unix search robtest.txt for anything that is in the 1[8-9]-0 range which is only 1899 and 1999. It couldn't be anything from the year 2000 to 2006. The 1 before the bracket specifies that the years can range from 1[8 which means 18, or 1[9, which specifies the second part of the year (the last two digits) The second bracket specifies the same thing. The 9 has one of them specified already—the 9. Now, apply the same concept. The 9 before the bracket 9] will specify the last two digits of the year range anywhere from either 9[0 which means 90, or 9[9, which specifies 1999. Once you have mastered this concept, it should be easier to apply more complex REs.

Using ranges can help you pull certain values out of files that you may need, such as the two years we just showed. You can expand the capability of the range by applying the negation operator as well. The character ^ negates a range if it is used at the start of the range specification. Negating a range will match the opposite of what the range matches.

For example, type the following:

```
grep "1-[8-9][0-9]*" robtest.txt
2006
2005
2004
2003
2002
2001
2000
1999
1999
```

## Using ^ and $

In this section, we will learn more about REs, particularly when using and negating ranges using the [] and ^ characters.

## Regular Expressions 163

You've noticed that the robtest.txt file you created and have been using the years 1899 through 1999 inside of it. We will use grep again in conjunction with REs to match the years that only fall in the 2000 range. To do this, you can specify a range using REs as: [<starting point--ending point]]. The starting and ending points can be numbers or ranges within the alphabet.

For example, type the following:

```
grep "1-[8-9][0-9]*" robtest.txt
1999
1899
```

This example lets Unix search robtest.txt for anything that is in the 1[8-9]-0 range which is only 1899 and 1999. It couldn't be anything from the year 2000 to 2006. The 1 before the bracket specifies that the years can range from 1[8 which means 18, or 1[9, which specifies the second part of the year (the last two digits) The second bracket specifies the same thing. The 9 has one of them specified already—the 9. Now, apply the same concept. The 9 before the bracket 9] will specify the last two digits of the year range anywhere from either 9[0 which means 90, or 9[9, which specifies 1999. Once you have mastered this concept, it should be easier to apply more complex REs.

Using ranges can help you pull certain values out of files that you may need, such as the two years we just showed. You can expand the capability of the range by applying the negation operator as well. The character ^ negates a range if it is used at the start of the range specification. Negating a range will match the opposite of what the range matches.

For example, type the following:

```
grep "1-[8-9][0-9]*" robtest.txt
2006
2005
2004
2003
2002
2001
2000
1999
1999
```

## Using ^ and $

In this section, we will learn more about REs, particularly when using and negating ranges using the [] and ^ characters.

In this section, we will learn more about REs, particularly when using and negating ranges using the [] and ^ characters.

In this section, we will learn more about REs, particularly when using and negating ranges using the [] and ^ characters.

In this section, we will learn more about REs, particularly when using and negating ranges using the [] and ^ characters.

In this section, we will learn more about REs, particularly when using and negating ranges using the [] and ^ characters.

In this section, we will learn more about REs, particularly when using and negating ranges using the [] and ^ characters.

## Using anchors:
- ^ matches the beginning of a line.
- $ matches the end of a line.

For example, examine how this is done:

```
>grep ^[7-8][0-9]* robtest.txt
1899
1999
```

This would have only shown me the dates I specified and nothing else, because I specified it clearly using grep and regular expressions.

## Summary

In this lesson, we covered the fundamentals of regular expressions, better known as REs. Regular expressions are an extremely flexible way of describing a pattern to be matched. Because many Unix applications, including the shell, support REs, it is important to develop a general understanding of how they work and what they are used for. With people relying on Unix (or Linux) as their server system or desktop of choice, knowing some of the power you can unleash will aid you in finding areas you need to study deeper, and this is definitely one of them. Here's a review:

- .matches any character. Use it whenever you're sure what character falls in a specific position.
- —Using the * matches any number of occurrences of a specific pattern. You can use this in conjunction with . or with ranges.
- \—Special characters need to be escaped using the \ character. If you need to use the quote character (*) in a pattern, you'll have to escape it.
- Ranges—You can match ranges of numbers or letters to limit a pattern. Ranges are enclosed in [] characters. To negate a range, use ^ at the beginning of the range specification.
- ^$/—These two special characters match the beginning and end of a line, respectively. They are commonly referred to as anchors because they hold a pattern to a specific place on a line.
