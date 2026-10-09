# **LAB 12**

# Archiving Files on the Command Line

**Lab Objective:**
Learn how to create, extract, and examine various types of archive files.

**Lab Purpose:**
In this lab, you will learn about zip, gzip, bzip2, and xz compressed archives—as well as a tool, called `tar`, to manage most Linux archive types.

**Lab Tool:**
Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**
A single Linux machine, or virtual machine

**Lab Walkthrough:**

***Task 1:***
Open the Terminal application and run the following:

```
```
mkdir lab12
cd lab12
touch f1 f2 f3 f4 f5 f6 f7 f8 f9
```
```

***Task 2:***
If you've worked with Windows, you may be familiar with ZIP files. ZIP is a common type of archive which both compresses and stores files.

Run:

```
```
zip files.zip f*
unzip -l files.zip
```
```

You can see that all nine files are included in files.zip, although since they were empty there was nothing to compress. You can unzip this archive with `unzip files.zip`, but you will be prompted to overwrite the existing files.