
## The init Process

  The first process, called `init` in Linux, is started by the kernel at boot time and never terminates. The PID of the `init` process is always 1.

## Foreground Processes

  A *foreground process* is a program with which a user is interacting at a particular time. Only one foreground process can be run at a time. As the user switches between programs, different programs become the foreground process at different times. A foreground process is initiated by entering a command at the prompt or by clicking a shortcut in the GUI.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_400_0.png)

## Background Processes

  A *background process* is a program that allows the Linux shell to execute a command that runs a job in the background, enabling processes to run simultaneously. While the user is interacting with the foreground process, a number of programs can run as background processes. The shell does not have to wait for one process to end before it can run more. A process can be run in the background by suffixing the invoking command with an ampersand ( & ) separated by a space.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_400_1.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_400_2.png)

*Figure 10-2: A process initiated to run in the background.*

## Daemons

  Daemons always run as background processes that never require user input. Other processes remain in the background temporarily, while the user is busy with the current foreground process.

## The Program and Process Relationship

  A *program* is a set of instructions describing how to carry out a task. A command that resides on your system is a program. When you enter a command at the prompt, a set of instructions perform a task.

  A process is a program that executes instructions. The operating system creates a process to carry out that task. Processes have unique identities and exist until their tasks are completed. When the task is completed, the process is terminated. Each program running on a system is assigned a PID.

## Multitasking

![](img/477ccb2f05b6ba1b2d563ea74f18c197_401_0.png)

**Definition:**

  *Multitasking* is a method of allowing the operating system to run concurrent programs simultaneously without degrading system performance. Multitasking enables several programs to share the same system resources. Processes spawned by multitasking are all active at the same time. They are not in a sequence or a suspended state, waiting to be run. Processes placed in a multitasking state remain active until completed, unless terminated or suspended by the user. One or more users may run multiple tasks on a system.

**Example:**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_401_1.png)

**Figure 10-3: Multitasking in a Linux system.**

## The Jobs Table

![](img/477ccb2f05b6ba1b2d563ea74f18c197_401_2.png)

  The *jobs table*, invoked by the `jobs` command, is a table containing information about jobs running in the background. It contains entries only for those jobs that are running in the current shell. The jobs table contains a numeric label for each job indicating the order in which the jobs were started. In addition, the jobs table includes a plus sign (+) to designate the current or most recently started job, and a minus sign (-) to designate the job that was started just prior to the most recent job. It also includes the status and name of each job.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_402_0.png)

*Figure 10-4: The jobs table listing jobs running in the current shell.*

  The job name listed in the jobs table is actually the command that initiated the job.

  The plus ( + ) and minus ( - ) signs indicate only the order in which jobs are started. All jobs, however, are actually being run simultaneously.

### Job Status

  There are four possibilities for the status of a job.

| Status | Description |
| :--- | :--- |
| Running | An active job. |
| Stopped | A job that has been suspended. |
| Terminated | A job that has been killed. |
| Done | A completed job. |

### Jobs in a New Shell

  Any job that a user placed in the background will appear in that user's jobs table, but other users' jobs will not appear. If you were to start a new shell, the jobs table for the new shell will be empty. However, the jobs started in the previous shell will continue to run.

## Suspend vs. Terminate a Process

  The Ctrl+Z key combination suspends a job, while the Ctrl+C key combination terminates or kills the job. If you display the jobs table after you press Ctrl+Z to suspend a job, you will see that the current job is in a suspended state (labeled in the jobs table as “Stopped”). Although the jobs table lists jobs running in the background, a foreground job that gets suspended appears in the jobs table to remind the user that there is a suspended job waiting to be restarted or terminated. Refer to the following table for a summary of job control commands.

| Action | Foreground | Background |
|---|---|---|
| Suspend a job | Ctrl+Z | Bring to foreground, then press Ctrl+Z |
| Terminate a job | Ctrl+C | kill %# |

## Restarting a Suspended Job

  The bg command, with the syntax bg { %#}, can be used to restart a specified background job that has been suspended. You can specify the number of the suspended job you want to restart after the percent sign. If there is only one job running in the background, then you don’t have to specify the number. You can type bg % to restart it.

## Bringing a Job to the Foreground

  If you need to bring a job from the background to the foreground, use the fg command, with the syntax fg { %#}. This command brings the specified job to the foreground. You don’t have to enter a number after the percent sign if there is only one job running in the background.

## Job Control Tools

![](img/477ccb2f05b6ba1b2d563ea74f18c197_403_0.png)

  Job control tools enable you to manipulate the jobs appearing on the jobs table.

| Tool | Enables You To |
|---|---|
| jobs | View the status of the jobs running in the background. |
| Ctrl+Z | Temporarily halt a running process. |
| fg { %job number} | Bring the specified process to the foreground. |
| bg { %job number} | Send the specified process to the background. |
| kill { %job number} | Terminate the specified process. |

## How to Manage Jobs and Background Processes

### Procedure Reference: Manage Jobs

To manage jobs:
1. Type the command with an ampersand ( `&` ) after it to put a job in the background.
2. If necessary, execute additional commands.
   - Execute another command in the background using the ampersand.
   - Or, execute another command without putting it in the background.
3. Enter `jobs` at the command line to see the list of processes that are running in the background.
4. Manage the jobs that are running in the background.
   - Enter `kill %[job number]` to kill a process in the background.
   - Enter `fg %[job number]` to switch a background process to the foreground. Suspend and restart the job.
     - a. Press `Ctrl+Z` to suspend a foreground job.
     - b. Enter `bg %[job number]` to restart a suspended job.

## ACTIVITY 10-1

### Managing Jobs

- **Before You Begin:**
  1. You have logged in as root in the CLI.
  2. The first terminal is displayed.

**Scenario:**

  As a system administrator, you are asked to conserve the amount of time it takes to run jobs on the Linux system. You need to manage multiple jobs instead of running one job at a time. You can accomplish this by moving jobs to be processed in the background.

- 1. **What You Do**: Issue three commands and put them in the background.

   **How You Do It**:
   a. Enter `sleep 300 &` to pause for 300 seconds.
   b. Enter `updatedb &` to update the mlocate database.
   c. Enter `sleep 200 &` to pause for 200 seconds.
   d. Enter `jobs` to view the list of processes running in the background.
   e. Verify that the three jobs are listed.

- 2. **What You Do**: Terminate the last job.

   **How You Do It**:
   a. Enter `kill %3` to kill the process that is executing the `sleep 200 &` command.
   b. Enter `jobs` to view the list of processes running in the background.
   c. Verify that the status of the third job displays “Terminated,” to indicate that the job has been terminated.
