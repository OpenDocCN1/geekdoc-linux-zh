# Tools and Utilities

There are many more commands available to ordinary users under Linux than you have seen so far. This chapter concentrates on some of the more sophisticated commands available, which singly or in combination make it possible to do many useful things without having to resort to any programming.

Many of the commands described in this chapter are designed to take their input from the standard input device and to send their output to the standard output device. This makes them ideal candidates to use when building up more complex pipelines, where the output from one command is piped into the input of the next. Commands of this type are generally called *filters*. These commands read their standard input, perform some transformation on it and then write the result to the standard output.

# 5.1 Search and Sort

A very common operation is to want to search through a file for lines containing a particular string, or to search through a list for a particular item. Another common operation is to sort lines into some kind of order. Linux has commands which can perform both of these actions either from the command line or from within a pipeline.

# 5.1.1 grep

The first command to look at is a filter called grep. The name is an acronym for *General Regular Expression Parser*, which translated into English means that grep can be used to search for string patterns in its input. The output from grep consists of all the lines of input which contained the specified string pattern. For example, to find out whether or not a login for the user carey exists on the system,