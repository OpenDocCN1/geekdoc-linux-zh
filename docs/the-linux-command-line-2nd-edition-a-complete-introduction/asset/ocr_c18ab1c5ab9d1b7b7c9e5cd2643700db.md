# 21 – Formatting Output

In this chapter, we continue our look at text-related tools, focusing on programs that are used to format text output, rather than changing the text itself. These tools are often used to prepare text for eventual printing, a subject that we will cover in the next chapter. The programs that we will cover in this chapter include:

+   - nl – Number lines
+   - fold – Wrap each line to a specified length
+   - fmt – A simple text formatter
+   - pr – Prepare text for printing
+   - printf – Format and print data
+   - groff – A document formatting system

# Simple Formatting Tools

We'll look at some of the simple formatting tools first. These are mostly single-purpose programs, and a bit unsophisticated in what they do, but they can be used for small tasks and as parts of pipelines and scripts.

# nl – Number Lines

The nl program is a rather arcane tool used to perform a simple task. It numbers lines. In its simplest use, it resembles cat -n:

```
[me@linuxbox ~]$ nl distros.txt | head
     1   SUSE      10.2   12/07/2006
     2   Fedora    10     11/25/2008
     3   SUSE      11.0   06/19/2008
     4   Ubuntu    8.04   04/24/2008
     5   Fedora    8      11/08/2007
     6   SUSE      10.3   10/04/2007
     7   Ubuntu    6.10   10/26/2006
```