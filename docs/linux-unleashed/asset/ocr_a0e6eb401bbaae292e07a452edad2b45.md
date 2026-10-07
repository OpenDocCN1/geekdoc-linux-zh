The string class adds UNIX shell type string operators to the C++ language, as well as a large number of additional operators. Table 27.4 lists many of the operators that are available with the string class.

# **TABLE 27.4. STRING CLASS OPERATORS.**

| Operator | Meaning |
| :------- | :------- |
| str1 == str2 | Returns TRUE if str1 is equal to str2 |
| str1 != str2 | Returns TRUE if str1 is not equal to str2 |
| str1 < str2 | Returns TRUE if str1 is less than str2 |
| str1 <= str2 | Returns TRUE if str1 is less than or equal to str2 |
| str1 > str2 | Returns TRUE if str1 is greater than str2 |
| str1 >= str2 | Returns TRUE if str1 is greater than or equal to str2 |
| compare(str1,str2) | Compares str1 to str2 without considering the case of the characters |
| str3 = str1 + str2 | Stores the result of str1 concatenated with str2 into str3 |



A number of other operators are available in the string class for performing different types of string comparisons, concatenations, and substring extraction and manipulation.

# # Random Numbers

Classes are provided in the GCC C++ class library that allow you to generate several different kinds of random numbers. The classes used to generate these numbers are the Random class and the RNG class.

# # Data Collection

The class library provides two different classes that perform data collection and analysis functions. The two classes are SampleStatistic and SampleHistogram. The SampleStatistic class provides a way of collecting samples and also provides numerous statistical functions that can perform calculations on the collected data. Some of the calculations that can be performed are mean, variance, standard deviation, minimum, and maximum.

The SampleHistogram class is derived from the SampleStatistic class and supports the collection and display of samples in bucketed intervals.