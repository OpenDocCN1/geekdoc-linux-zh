![](bbox=[0.105, 0.063, 0.378, 0.215])

# # LESSON 13

# # Regular Expressions

In this lesson, you will learn the basics of regular expressions and how to use them in your Unix environment.

As we learn more about Unix, it is apparent that most of its power comes from commands such as cron, ls, man, tail, and so on. And what did we learn in the last lesson? We learned how commands can be combined or altered based on other characters added, which would specify tasks for Unix. In this chapter, we will continue this discussion, as I will introduce you to the concept of regular expressions.

Regular expressions, commonly known as "RE, RegEx, regexp, or regexp," are a set of key combinations that allow Unix users and administrators to have control over what they are searching for when using commands such as grep. Regular expressions are used in conjunction with other commands.

Text editors (like vi) and utilities use regular expressions to search and manipulate bodies of text based on certain patterns. Many programming languages, such as Perl, support REs for string manipulation. For example, Perl has a powerful RE engine built directly into its syntax. Although in this lesson you'll be looking primarily at the grep command used in conjunction with REs, you can apply this knowledge to almost everything that uses REs.

# # Pattern Matching and Regular Expressions

In earlier lessons, you were introduced to the use of the wildcard symbol (*), used to help you find files that you need, or to find contents within