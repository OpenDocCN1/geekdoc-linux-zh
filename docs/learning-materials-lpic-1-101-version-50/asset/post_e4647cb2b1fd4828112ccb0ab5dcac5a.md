
# Answers to Guided Exercises

-   1. It’s convenient to save the execution date of actions performed by automated scripts. Command `date +%Y-%m-%d` shows the current date in year-month-day format. How can the output of such a command can be stored in a shell variable called `TODAY` using command substitution?

    ```bash
    $ TODAY=`date +%Y-%m-%d`
    ```
    
    or
    
    ```bash
    $ TODAY=$(date +%Y-%m-%d)
    ```

-   2. Using command `echo`, how can the contents of variable `TODAY` be sent to the standard input of command `sed s/-/.g`?

    ```bash
    $ echo $TODAY | sed s/-/.g
    ```

-   3. How could the output of command `date +%Y-%m-%d` be used as a Here string to command `sed s/-/.g`?

    ```bash
    $ sed s/-/.g <<< `date +%Y-%m-%d`
    ```
    
    or
    
    ```bash
    $ sed s/-/.g <<< $(date +%Y-%m-%d)
    ```

-   4. Command `convert image.jpeg -resize 25% small/image.jpeg` creates a smaller version of `image.jpeg` and places the resulting image in a likewise named file inside subdirectory `small`. Using `xargs`, how is it possible to perform the same command for every image listed in file `filelist.txt`?

    ```bash
    $ xargs -I IMG convert IMG -resize 25% small/IMG < filelist.txt
    ```
    
    or
    
    ```bash
    $ cat filelist.txt | xargs -I IMG convert IMG -resize 25% small/IMG
    ```

## Answers to Explorational Exercises

1.  A simple backup routine periodically creates an image of partition `/dev/sda1` with `dd < /dev/sda1 > sda1.img`. To perform future data integrity checks, the routine also generates a SHA1 hash of the file with `sha1sum < sda1.img > sda1.sha1`. By adding pipes and command `tee`, how would these two commands be combined into one?

    ```bash
    $ dd < /dev/sda1 | tee sda1.img | sha1sum > sda1.sha1
    ```

2.  Command `tar` is used to archive many files into a single file, preserving directory structure. Option `-T` allows to specify a file containing the paths to be archived. For example, `find /etc -type f | tar -cJ -f /srv/backup/etc.tar.xz -T -` creates a compressed tar file `etc.tar.xz` from the list provided by command `find` (option `-T -` indicates the standard input as the path list). In order to avoid possible parsing errors due to paths containing spaces, what command options should be present for `find` and `tar`?

    Options `-print0` and `--null`:

    ```bash
    $ find /etc -type f -print0 | tar -cJ -f /srv/backup/etc.tar.xz --null -T -
    ```

3.  Instead of opening a new remote shell session, command `ssh` can just execute a command indicated as its argument: `ssh user@storage "remote command"`. Given that `ssh` also allows to redirect the standard output of a local program to the standard input of the remote program, how would the `cat` pipe a local file named `etc.tar.gz` to `/srv/backup/etc.tar.gz` at `user@storage` through `ssh`?

    ```bash
    $ cat etc.tar.gz | ssh user@storage "cat > /srv/backup/etc.tar.gz"
    ```
    
    or
    
    ```bash
    $ ssh user@storage "cat > /srv/backup/etc.tar.gz" < etc.tar.gz
    ```

![image](img/824749d5fc1d265354d0e66a01af9ced_297_0.png)

## 103.5 Create, monitor and kill processes

**Reference to LPI objectives**

| Category | Details |
| :--- | :--- |
| Exam | LPIC-1 v5, Exam 101 |
| Objective | 103.5 |
| Weight | 4 |

**Key knowledge areas**

-   Run jobs in the foreground and background.
-   Signal a program to continue running after logout.
-   Monitor active processes.
-   Select and sort processes for display.
-   Send signals to processes.

**Partial list of the used files, terms and utilities**

-   `&`
-   `bg`
-   `fg`
-   `jobs`
-   `kill`
-   `nohup`
-   `ps`
-   `top`
-   `free`
-   `uptime`
-   `pgrep`
-   `pkill`
-   `killall`
-   `watch`
-   `screen`
-   `tmux`

![image](img/824749d5fc1d265354d0e66a01af9ced_299_0.png)

# 103.5 Lesson 1

| | | |
| :--- | :--- | :--- |
| **Certificate:** | LPIC-1 |
| **Version:** | 5.0 |
| **Topic:** | 103 GNU and Unix Commands |
| **Objective:** | 103.5 Create, monitor and kill processes |
| **Lesson:** | 1 of 2 |

## Introduction

Every time we invoke a command, one or more processes are started. A well-trained system administrator not only needs to create processes, but also be able to keep track of them and send them different types of signals if and when required. In this lesson we will look at job control and how to monitor processes.

## Job Control

*Jobs* are processes that have been started interactively through a terminal, sent to the background and have not yet finished execution. You can find out about the active jobs (and their status) in your Linux system by running *jobs*:

```bash
$ jobs
```

The *jobs* command above did not produce any output, which means there are no active jobs at the moment. Let us create our first job by running a command that takes some time to finish executing (the `sleep` command with a parameter of 60) and — while running — press `Ctrl` + `Z`:

```bash
$ sleep 60
^Z
[1]+  Stopped                 sleep 60
```

The execution of the command has been stopped (or — rather — suspended) and the command prompt is available again. You can look for jobs a second time and will find the *suspended* one now:

```bash
$ jobs
[1]+  Stopped                 sleep 60
```

Let us explain the output:

-   `[1]`
    This number is the job ID and can be used — preceded by a percentage symbol (%) — to change the job status by the `fg`, `bg` and `kill` utilities (as you will be shown later).
-   `+`
    The plus sign indicates the current, default job (that is, the last one being suspended or sent to the background). The previous job is flagged with a minus sign (-). Any other prior jobs are not flagged.
-   `Stopped`
    Description of the job status.
-   `sleep 60`
    The command or job itself.

With the `-l` option, jobs will additionally display the process ID (PID) right before the status:

```bash
$ jobs -l
[1]+  Stopped  1114 sleep 60
```

The remaining possible options of `jobs` are:

-   `-n`
    Lists only processes that have changed status since the last notification. Possible status include, Running, Stopped, Terminated or Done.
-   `-p`
    Lists process IDs.
-   `-r`
    Lists only running jobs.
-   `-s`
    Lists only stopped (or suspended) jobs.

**NOTE** Remember, a job has both a *job ID* and a *process ID* (PID).

## Job Specification

The `jobs` command as well as other utilities such as `fg`, `bg` and `kill` (that you will see in the next section) need a job specification (or *jobspec*) to act upon a particular job. As we have just seen, this can be—and normally is—the job ID preceded by %. However, other job specifications are also possible. Let us have a look at them:

-   **%n**
    Job whose id number is n:

    ```bash
    $ jobs %1
    [1]+  Stopped              sleep 60
    ```

-   **%str**
    Job whose command line starts with *str*:

    ```bash
    $ jobs %sl
    [1]+  Stopped              sleep 60
    ```

-   **%?str**
    Job whose command line contains *str*:

    ```bash
    $ jobs %?le
    [1]+  Stopped              sleep 60
    ```

-   **%+ or %%**
    Current job (the one that was last started in the background or suspended from the foreground):

    ```bash
    $ jobs %+
    [1]+  Stopped     sleep 60
    ```

-   **%-**
    Previous job (the one that was %+ before the default, current one):

    ```bash
    $ jobs %-
    [1]+  Stopped     sleep 60
    ```

In our case, since there is only one job, it is both current and previous.

## Job Status: Suspension, Foreground and Background

Once a job is in the background or has been suspended, we can do any of three things to it:

1.  Take it to the foreground with `fg`:

    ```bash
    $ fg %1
    sleep 60
    ```

    `fg` moves the specified job to the foreground and makes it the current job. Now we can wait until it finishes, stop it again with `Ctrl + Z` or terminate it with `Ctrl + C`.

2.  Take it to the background with `bg`:

    ```bash
    $ bg %1
    [1]+ sleep 60 &
    ```

    Once in the background, the job can be brought back into the foreground with `fg` or killed (see below). Note the ampersand (&) meaning the job has been sent to the background. As a matter of fact, you can also use the ampersand to start a process directly in the background:

    ```bash
    $ sleep 100 &
    [2] 970
    ```

    Together with the job ID of the new job ([2]), we now get its process ID (970) too. Now both
