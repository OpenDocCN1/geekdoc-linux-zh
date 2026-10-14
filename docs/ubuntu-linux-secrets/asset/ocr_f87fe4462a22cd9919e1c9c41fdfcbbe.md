To access the values in a hash variable, you need to know the individual key values, and, like array index numbers, you must enclose them in square brackets:

```
irb(main):007:0> test = {"key1"=>"value1","key2"=>"value2","key3"=>"value3"}
-> {"key3"=>"value3","key1"=>"value1","key2"=>"value2"}
irb(main):008:0> name["key1"]
-> "value1"
irb(main):009:0>
```

But what if you don't know what keys are in a hash? Fortunately, there's a simple solution. When working with hashes, if you don't know the key name you can't write the code to access the value. Ruby provides an iterator for hashes to help solve this problem.

The hash iterator works the same as the array iterator but with a twist. You can extract the key as well as the value in each iteration. The hash iterator uses the format:

```
hash.each do |key, value|
  statements to execute
end
```

Let's work on an example to demonstrate the procedure:

+   1. Open a text editor and enter the following code:
+      information = { "city" => "Chicago," "state" => "Illinois," "zip" => "60633" }
+      information.each do |key, value|
+        puts key + ": " + value
+      end
+   2. Save the file as hashtest.rb in your home folder.
+   3. Open a Terminal session and run the code using the Ruby interpreter.

When you see the output from this process, you might be surprised:

```
$ ruby hashtest.rb
city: Chicago
zip: 60633
state: Illinois
$
```

The keys aren't listed in the same order in which we created them! This is a drawback to using hashes. It's not guaranteed that the hash iterator will return the hash elements in the same order, so don't count on it in your program! If you require your data to appear in the same order, you need to write extra Ruby code to store the output of the iterator and display it appropriately.

# Structured Commands

As with the other programming languages, Ruby supports a set of structured commands that allow you to alter the flow of the program based on a condition. This section discusses the two most popular structured commands used in Ruby.

# The if-then Statements

The most common structured command you'll see in Ruby programming is the if-then statement. The if-then statement checks the result of a condition and then performs a