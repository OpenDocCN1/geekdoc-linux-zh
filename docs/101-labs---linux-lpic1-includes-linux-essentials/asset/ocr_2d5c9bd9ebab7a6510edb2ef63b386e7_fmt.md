
# LAB 52

## Search Text Files Using Regular Expressions: Basic Regex

**Lab Objective:**

Learn how to use basic regular expressions for complex string pattern matching.

**Lab Purpose:**

Regular expressions are a tool used commonly in Linux to match complex patterns in strings and text files. Many tools support regular expressions. With basic regex, some metacharacters require backslashes in front of them.

**Lab Tool:**

`Ubuntu 18.04` (or another distro of your choice)

**Lab Topology:**

A single Linux machine, or virtual machine

**Lab Walkthrough:**

*Task 1:*

Open the `Terminal` application and create a text file first (copy and paste won't work for the below):

```
echo "abc123
456def
<html>
Hello World!
password
01234567890
A1B2C3D4E5
6F7G8H9I0J
Quoth the raven: "Nevermore." > lab52.txt
```
