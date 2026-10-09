# **LAB 81**

# System Logging: Rsyslog

**Lab Objective:**  
Learn how to configure the `rsyslog` logging daemon.

**Lab Purpose:**  
In this lab, you will learn about basic configuration of `rsyslog` and its different logging options.

**Lab Tool:**  
Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**  
A single Linux machine, or virtual machine

**Lab Walkthrough:**

+   *Task 1:*  
+   Open two Terminal windows/tabs.

In the first one, run: `tail -f /var/log/syslog`

In the second one, run: `logger "Hello World"`

Now go back to the first tab. Did your friendly message show up in the system logs? Hit Ctrl+C to exit `tail`.

> `logger` is a generic utility for sending logs to a number of daemons, including `rsyslog`, and `journal` which we will discuss in Lab 83.

+   *Task 2:*  
+   Now look at the configuration:

```
grep -v -e ^# -e ^$ /etc/rsyslog.conf /etc/rsyslog.d/*
```