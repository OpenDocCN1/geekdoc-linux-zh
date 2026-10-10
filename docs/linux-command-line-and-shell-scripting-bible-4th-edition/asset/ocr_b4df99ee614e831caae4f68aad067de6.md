# # CHAPTER 20
# Regular Expressions

# IN THIS CHAPTER

+   * Exploring regular expressions
+   * Defining BRE patterns

Trying out extended regular expressions The key to successfully working with sed and gawk in your shell script is your comfort using regular expressions. This is not always an easy thing to do, because trying to filter specific data from a large batch of data can (and often does) get complicated. This chapter describes how to create regular expressions in both sed and gawk that can filter out just the data you need.

# ## Exploring Regular Expressions

The first step to understanding regular expressions is to define just exactly what they are. This section explains what a regular expression is and describes how Linux uses regular expressions.

# ## A definition

A regular expression is a pattern template you define that a Linux utility uses to filter text. A Linux utility (such as sed or gawk) matches the regular expression pattern against data as that data flows into the utility. If the data matches the pattern, it's accepted for processing. If the data doesn't match the pattern, it's rejected. This is illustrated in Figure 20-1.

The regular expression pattern makes use of wildcard characters to represent one or more characters in the data stream. There are plenty of instances in Linux where you can specify a wildcard character to represent data you don't know about. You've already seen an example of using wildcard characters with the Linux ls command for listing