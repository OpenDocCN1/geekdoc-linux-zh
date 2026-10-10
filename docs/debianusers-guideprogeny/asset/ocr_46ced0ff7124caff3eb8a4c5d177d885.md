Within a string, you can type in multiple words, or disable metacharacters (also known as wild cards). A string that uses metacharacters is referred to as a regular expression. See “Using Metacharacters or Wild Cards,” page 118.

If you use double straight quotation marks, all metacharacters are disabled except environment variables, such as $HOME.

Single straight quotation marks disable all special characters. In most cases, use single quotation marks.

Do not use true quotation marks (“ ”). True quotation marks may be a problem if you copy and paste from a word processor.

For example, if you wanted to search user jsmith’s home directory for a file that contained the phrase “business expenses,” you would use the grep command with the phrase as an argument: grep 'business expenses' /home/jsmith/.

# **Using Metacharacters or Wild Cards**

Metacharacters are characters that designate a range of choices. They are also called special characters or wild cards.

You may know the basic metacharacters from other operating systems:

+   ▼ A asterisk (*) includes any number of characters.
+   ▼ A question (?) mark includes any single character.

**Warning**
Metacharacters can be extremely powerful, especially when used in combination. Be careful about using them when you are deleting and copying files.