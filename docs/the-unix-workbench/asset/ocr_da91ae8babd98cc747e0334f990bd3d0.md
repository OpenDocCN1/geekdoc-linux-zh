back a weather report given a location). Building these kinds of servers is an advanced topic that is outside the scope of this book, but there are lots of resources out there if you’re interested in building your own HTTP API on a web server.

# Automating Tasks

One of the most compelling features about any web server is that it’s always powered on and always connected to the internet. This means that we can instruct our server to perform tasks automatically, without us needing to enter a command into a shell. One of the most commonly used programs for executing *other programs* with a regular frequency is called `cron`. Let’s take a look at how to use cron to schedule a program to be run.

If you’re not already connected to the server use `ssh` to connect.

```
ssh root@159.203.134.88
```

The `cron` program is part of a family of programs called **daemons**. A daemon is a program that is always running in the background of our computer. First, let’s see if cron is running. We can get a list of all running programs with the `ps` command while using the -A flag:

```
ps -A
```