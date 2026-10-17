
# LAB 78

## Localisation and Internationalisation: Locales

### Lab Objective

Learn how to configure locale settings.

### Lab Purpose

In this lab, you will learn how locales work in Linux and how to configure their settings and environment variables.

### Lab Tool

`Ubuntu 18.04` (or another distro of your choice)

### Lab Topology

A single Linux machine, or virtual machine

### Lab Walkthrough

**Task 1:**

Open the Terminal and run: `locale`

You should see a number of variables, the first of which being `LANG`—as you might guess, this is the locale setting for your default language. Several other variables are listed below it, naming the settings for dates/times, phone numbers, currency, and other designations.

To see the locale settings currently supported by your system: `locale -a`

And to see supported character maps: `locale -m`

Your default locale settings are probably some variation of `UTF-8`, which is a standard character map on Linux.
