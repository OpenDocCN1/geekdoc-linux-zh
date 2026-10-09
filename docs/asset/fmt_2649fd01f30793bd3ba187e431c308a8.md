
# LAB 76

## Automate System Administration Tasks by Scheduling Jobs: `at` and `Systemd`

### Lab Objective

Learn how to use `at` and `Systemd` utilities to schedule automated system tasks.

### Lab Purpose

In this lab, you will manage automated system tasks with `Systemd` and scheduled tasks using `at`.

### Lab Tool

`Ubuntu` 18.04 (or another distro of your choice)

### Lab Topology

A single Linux machine, or virtual machine

### Lab Walkthrough

#### Task 1

Open the Terminal and run: `sudo apt install at`

In contrast to `cron`, `at` is used for running one-time jobs at some time in the future.

Now run:

- `echo "touch foo" | at now + 1 min`
- `atq`
- `sleep 60 && ls foo`
- `rm foo`

You scheduled a `touch foo` command to be run in the future; `atq` shows this job (which you could delete if you wanted to, using `atrm`). One small caveat, though—`at` will not necessarily schedule your job *exactly* one minute in the future, when used with this syntax. The seconds are truncated, so, in fact, it may run less than one second from “now,” `at` isn’t generally used in scenarios requiring such precision!
