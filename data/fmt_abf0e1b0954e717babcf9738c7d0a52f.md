
# LAB 94

# Configure Client-Side DNS: dnsutils

**Lab Objective:**

Learn how to use classic Linux utilities to configure client-side DNS.

**Lab Purpose:**

In this lab you will work with classic tools such as `dig` to configure and troubleshoot DNS resolution.

**Lab Tool:**

Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**

A single Linux machine, or virtual machine

**Lab Walkthrough:**

### Task 1

In ye olden days, one could just `cat /etc/hosts /etc/resolv.conf` and gather all the DNS information one needed. This is, sadly, no longer true. Instead, run `nmcli` to find out what your current DNS servers are (see “DNS configuration” near the bottom), then save these for later. You probably have two nameservers, which will be referred to as `[dns1]` and `[dns2]` below.

### Task 2

Now you will experiment with `dig`, one of the most common and useful DNS troubleshooting utilities:

- `dig 101labs.net`
- `dig 101labs.net MX +short`
- `dig CNAME www.101labs.net [dns1]`
- `dig AAAA example.com [dns2] +short`
