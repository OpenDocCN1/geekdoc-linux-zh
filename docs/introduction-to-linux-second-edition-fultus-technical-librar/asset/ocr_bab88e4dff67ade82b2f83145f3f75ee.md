# 5.3 Filters

When a program performs operations on input and writes the result to the standard output, it is called a filter. One of the most common uses of filters is to restructure output. We'll discuss a couple of the most important filters below.

# 5.3.1 More about grep

As we saw in Section 3.3.3.4, **grep** scans the output line per line, searching for matching patterns. All lines containing the pattern will be printed to standard output. This behavior can be reversed using the *-v* option.

Some examples: suppose we want to know which files in a certain directory have been modified in February:

```
jenny:~> ls -la | grep Feb
```

The **grep** command, like most commands, is case sensitive. Use the *-i* option to make no difference between upper and lower case. A lot of GNU extensions are available as well, such as *--colour*, which is helpful to highlight searchterms in long lines, and *--after-context*, which prints the number of lines after the last matching line. You can issue a recursive **grep** that searches all subdirectories of encountered directories using the *-r* option. As usual, options can be combined.

Regular expressions can be used to further detail the exact character matches you want to select out of all the input lines. The best way to start with regular expressions is indeed to read the **grep** documentation. An excellent chapter is included in the **grep** Info page. Since it would lead us too far discussing the ins and outs of regular expressions, it is strongly advised to start here if you want to know more about them.

Play around a bit with **grep**, it will be worth the trouble putting some time in this most basic but very powerful filtering command. The exercises at the end of this chapter will help you to get started, see Section 5.5.

# 5.3.2 Filtering output

The command **sort** arranges lines in alphabetical order by default:

```
thomas:~> cat people-I-like | sort
Auntie Emmy
Boyfriend
Dad
Grandma
Mum
My boss
```