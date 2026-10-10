# ## CHAPTER
## 22
# Advanced gawk

# IN THIS CHAPTER

+   - Using variables
+   - Working with arrays
+   - Considering patterns
+   - Understanding structured commands
+   - Printing with formats
+   - Using built-in functions
+   - Trying out user-defined functions

C hapter 19, “Introducing sed and gawk,” introduced the gawk program and demonstrated the basics of using it to produce formatted reports from raw data files. This chapter dives more deeply into customizing gawk to produce reports. The gawk program is a full-fledged programming language, providing features that allow you to write advanced programs to manipulate data. If you are jumping into the shell script world from another programming language, you should feel right at home with gawk. In this chapter, you see how to use the gawk programming language to write programs to handle just about any data-formatting task you’ll run into.

# ## Using Variables

One important feature of any programming language is the ability to store and recall values using variables. The gawk programming language supports two different types of variables:

+   - Built-in variables
+   - User-defined variables

Several built-in variables are available for you to use in gawk. The built-in variables contain information used in handling the data fields and records in the data file. You can also create your own variables in your gawk programs. The following sections walk you through how to use variables in your gawk programs.