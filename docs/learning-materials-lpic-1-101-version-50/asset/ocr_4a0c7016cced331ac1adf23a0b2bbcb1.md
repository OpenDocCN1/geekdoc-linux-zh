![](bbox=[0.59, 0.07, 0.92, 0.2])

# 103.7 Lesson 2

| Certificate: | LPIC-1 |
|---|---|
| Version: | 5.0 |
| Topic: | 103 GNU and Unix Commands |
| Objective: | 103.7 Search text files using regular expressions |
| Lesson: | 2 of 2 |

# Introduction

Streaming data through a chain of piped commands allows for the application of compound filters based on regular expressions. Regular expressions are an important technique used not only in system administration, but also in data mining and related areas. Two commands are specially suited to manipulate files and text data using regular expressions: grep and sed. grep is a pattern finder and sed is a stream editor. They are useful by themselves, but it is when working together with other processes that they stand out.

# The Pattern Finder: grep

One of the most common uses of grep is to facilitate the inspection of long files, using the regular expression as a filter applied to each line. It can be used to show only the lines starting with a certain term. For example, grep can be used to investigate a configuration file for kernel modules, listing only option lines:

```
```
$ grep 'options' /etc/modprobe.d/alsa-base.conf
options snd-pcsp index=-2
options snd-usb-audio index=-2
```
```