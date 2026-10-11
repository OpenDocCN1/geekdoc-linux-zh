# Tutorial

# Hash tables

![](bbox=[0.06, 0.16, 0.18, 0.26])

Mihalis Tsoukalos
is a Unix administrator, a programmer (for Unix and iOS), a DBA and also a maintainer. He has been using Linux since 1993.

# Resources

Text editor
GCC compiler

![](bbox=[0.06, 0.75, 0.18, 0.84])

Tutorial files available:
filessilo.co.uk

# Computer science: Find strings with hash tables

> Take the time to learn how to use hash tables and discover how they make your life easier

Hash tables are a key component of computing and programming languages; they are being supported in almost any programming language, including AWK. Strictly speaking, a hash table is a data structure that stores one or more key and value pairs. A hash table uses a hash function to compute an index into an array of buckets, or slots, from which the correct value can be discovered. Ideally, the hash function will assign each key to a unique bucket, provided that you have the required number of buckets. As you will see, this rarely happens. In practice, more than one key will hash at the same bucket. The worst restriction of a hash table is that once you define the hash function and the number of buckets, neither of these two properties can be changed without rebuilding the entire hash table. Therefore the best thing you can do to make a hash table faster is to increase the number of buckets and make sure that the hash function uses all buckets! The hypothetical problem that you are going to solve here is to find out whether a word can be found in a dictionary or not - this is an operation that has to occur fast.

All C programs will be compiled as follows:
`$ gcc -Wall programName.c -o programName`

# The theoretical part

The single most important characteristic of a hash table is the number of buckets used by the hashing function. The second most important characteristic is the hash function itself. The most crucial feature of the hash function is that it should produce a uniform distribution of the hash values, as it is inefficient to have unused buckets or big differences in the cardinalities of the buckets (see the page 52 image). Having n keys and k buckets means that the search speed goes from O(n) for a linear search to O(n/k). Although the improvement might look small, you should realise that for a hash array with only 30 buckets, the search time would be 30 times smaller! The diagram on the next page shows a simple yet fully characteristic hash table. The only problem with it is that it has a poorly chosen hash function, which does not return hash values that will fill all available buckets - as you can