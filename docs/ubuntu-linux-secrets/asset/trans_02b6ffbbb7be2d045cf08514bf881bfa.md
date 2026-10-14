

block of code depending on the value of the result. This feature allows you to control the operation of the program based on real-time data values.

Here's the basic format of the if-then statement:

```
if condition
statements to execute
end
```

If the condition results in a true Boolean value, Ruby executes the statements that appear before the end keyword. If the condition results in a false value, Ruby skips the statements and continues with the code immediately after the end keyword. Here's an example:

```
if num > 5
  puts "The value is larger than 5"
end
```

If we ran this code, we'd see that the string "The value is larger than 5" appears only if the variable num contains a value of 6 or greater. If the value is 5 or less, Ruby doesn't execute the puts statement.

## Comparing Data Types

The condition is the core of the if-then statement. You can use conditions to compare just about any data type and value. However, Ruby does have specific rules for comparing data types.

Unlike some of the other scripting languages (like Perl), Ruby uses the same comparator symbols for both numerical and text values. These symbols are shown in Table 29-2.

Table 29-2: Ruby Comparator Symbols

| Description | Symbol |
| Equals | == |
| Not equal | != |
| Less than | < |
| Greater than | > |
| Less than or equal | <= |
| Greater than or equal | >= |

Ruby can determine the data type used in the comparison and act accordingly. Even without running it, you can probably figure out the result you'd get from this code:

```
value1 = 50
value2 = 100
if value2 > value1
  puts "The value is larger"
end
```

In the example, both values in the condition are numerical. Here's an example of code that uses a condition to compare text values:

```
value = "testing"
if value == "testing"
  puts "This is only a test"
end
```

The string comparator operators allow you to easily compare string values in your programs. What gets tricky is when you use the greater-than and less-than comparators with strings. How do you know whether the word banana is less than or greater than the word orange? Ruby uses the alphabetical order of text characters to perform the comparison. An a character is 1, a b character is 2, and so on through the alphabet. So, for example, the word banana is less than the word orange.

## The if-then-else Statement

You’ll often need to execute one set of statements when a condition is true and another set of statements when it’s false. The else keyword is used to provide an alternate set of statements for Ruby to execute, like this:

```
if condition
  statements to execute if true
else
  statements to execute if false
end
```

In this format, if the condition is true, Ruby executes only the code between the if statement and the else keyword. You can put more than one statement in each section of the if-then-else code.

```
if price > 100
  price = price * .90
  puts "The new price is " + price.to_s
else
  price = price * .95
  puts "The new price is " + price.to_s
end
```

This example demonstrates checking to see whether the price variable value is larger than 100. If the price value is larger than 100, the price is changed to discount it by 10 percent (by multiplying by .90), and the result is displayed on the monitor (you need to use the .to_s method to convert the integer value into a string value to display it). If the price isn’t greater than 100, the else block of code implements a 5 percent discount, then displays the new price.

## The elsif Keyword

You can expand on the functionality of the if-then statement by stringing if-then statements together using the elsif keyword:

```
value = rand(100)
if value > 50
  puts "The value is big: " + value.to_s
elsif value > 25
```

```
puts "The value is medium: " + value.to_s
else
puts "The value is small: " + value.to_s
end
```

That’s quite a string of options! Often it’s hard to follow along in the elsif statement string. Let’s create an example using this code and walk through it:

- 1. Open a text editor and enter the following code:
- value = rand(100)
- if value > 50
- puts "The value is big: " + value.to_s
- elsif value > 25
- puts "The value is medium: " + value.to_s
- else
- puts "The value is small: " + value.to_s
- end
- 2. Save the file as iftest.rb in your home folder.
- 3. Open a Terminal session and run the code file using the Ruby interpreter.

The rand() function picks a random number from 0 to 100 and assigns it to the variable called value in our code example. Ruby walks through the if-then conditions and displays the appropriate message based on the value of the random number.

```
$ ruby iftest.rb
The value is big: 93
$ ruby iftest.rb
The value is medium: 29
$
```

The elsif makes trying to check multiple conditions considerably easier.

## The Loop Statements

Loops are another popular way to alter the flow of a program. Loops do what the name implies: They loop through a block of code for a predetermined number of times. This is a handy feature if you’re trying to loop through an equation a set number of times, such as as in a counter.

## Times Loops

Ruby has a unique way of implementing simple loops, called the times method. The times method can be used on both variables and constant numerical values. Here’s an example:

```
5.times do
  statements to execute
end
```

If you’re familiar with other programming languages, this may seem somewhat odd, but if you read the line of code, it makes perfectly good sense. The block of statements will repeat five times, just like the code says.

If you need to increment or decrement a variable value inside a loop, you have to manually create it and process it inside the loop. Try this example:

```
counter = 1
5.times do
```
