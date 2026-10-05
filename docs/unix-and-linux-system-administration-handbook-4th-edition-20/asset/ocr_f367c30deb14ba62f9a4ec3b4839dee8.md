# Chapter 2 Scripting and the Shell

# Special characters

Table 2.4 shows the meanings of some common special symbols that can appear in regular expressions. These are just the basics—there are many, many more.

# Table 2.4 Special characters in regular expressions (common ones)

a. That is, a space, a form feed, a tab, a newline, or a return

Many special characters, such as + and |, affect the matching of the "thing" to their left or right. In general, a "thing" is a single character, a subpattern enclosed in parentheses, or a character enclosed in square brackets. For the | character, however, thickness extends indefinitely to both left and right. If you want to limit the scope of the vertical bar, enclose the bar and both in their own set of parentheses. For example,

I am the (walruseggman).

matches either "I am the walrus." or "I am the egg man.". This example also demonstrates escaping of special characters (here, the dot). The pattern

(I am the (walruseggman)\.?[1,2)

matches any of the following:

+   * I am the walrus.
* I am the egg man.
* I am the walrus. I am the egg man.
* I am the egg man. I am the walrus.