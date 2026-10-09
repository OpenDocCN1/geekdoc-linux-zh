
preferences by which the different owners have allowed their machines to participate in the Condor pool.

After a job is submitted to Condor, a job ClassAd is created. This ClassAd includes attributes about the job, such as the amount of memory the job uses, the name of the program to run, the user who submitted the job, and the time it was submitted. The job can also specify requirements and preferences (or *rank*) for the machine that will run the job. For instance, perhaps you are looking for the fastest floating-point performance available. You want Condor to rank available machines based on floating-point performance. Perhaps you care only that the machine has a minimum of 256 MBytes of RAM. Or, perhaps you will take any machine you can get! These job attributes and requirements are bundled up into a job ClassAd.

Condor plays the role of matchmaker by continuously reading all the job ClassAds and all the machine ClassAds, matching and ranking job ads with machine ads. Condor ensures that the requirements in both ClassAds are satisfied.

### Structure of a ClassAd

A ClassAd is a set of uniquely named expressions. Each named expression is called an *attribute*. Each attribute has an *attribute name* and an *attribute value*. The attribute value can be a simple integer, *string*, or floating-point value, such as:

```text
Memory = 512
OpSys = "LINUX"
NetworkLatency = 7.5
```

An attribute value can also consist of a logical expression that will evaluate to TRUE, FALSE, or UNDEFINED. The syntax and operators allowed in these expressions are similar to those in C or Java, that is, `==` for equals, `!=` for not equals, `&&` for logical and, `||` for logical or, and so on. Furthermore, ClassAd expressions can incorporate attribute names to refer to other attribute values. For instance, consider the following small sample ClassAd:

```text
MemoryInMegas = 512
MemoryInBytes = MemoryInMegas * 1024 * 1024
Cpus = 4

BigMachine = (MemoryInMegas > 256) && (Cpus >= 4)
VeryBigMachine = (MemoryInMegas > 512) && (Cpus >= 8)
FastMachine = BigMachine && SpeedRating
```

In this example, *BigMachine* evaluates to TRUE and *VeryBigMachine* evaluates to FALSE. But, because attribute *SpeedRating* is not specified, *FastMachine* would evaluate to UNDEFINED.

Condor provides *meta-operators* that allow you to explicitly compare with the UNDEFINED value by testing both the type and value of the operands. If both the types and values match, the two operands are considered *identical*; `=?=` is used for meta-equals (or, is-identical-to) and `!=!` is used for meta-not-equals (or, is-not-identical-to). These operators always return TRUE or FALSE and therefore enable Condor administrators to specify explicit policies given incomplete information.

A complete description of ClassAd semantics and syntax is documented in the Condor manual.

**Matching ClassAds.** ClassAds can be matched with one another. This is the fundamental mechanism by which Condor matches jobs with machines. Figure 14.1 displays a ClassAd from Condor representing a machine and another representing a queued job. Each ClassAd contains a `MyType` attribute, describing what type of resource the ad represents, and a `TargetType` attribute. The `TargetType` specifies the type of resource desired in a match. Job ads want to be matched with machine ads and vice versa.

Each ClassAd engaged in matchmaking specifies a **Requirements** and a **Rank** attribute. In order for two ClassAds to match, the **Requirements** expression in both ads must evaluate to TRUE. An important component of matchmaking is the fact that the **Requirements** and **Rank** expression can refer not only to attributes in their own ad but also to attributes in the candidate matching ad. For instance, the **Requirements** expression for the job ad specified in Figure 14.1 refers to `Arch`, `OpSys`, and `Disk`, which are all attributes found in the machine ad.

What happens if Condor finds more than one machine ClassAd that satisfies the constraints specified by **Requirements**? That is where the **Rank** expression comes into play. The **Rank** expression specifies the desirability of the match (where higher numbers mean better matches). For example, the job ad in Figure 14.1 specifies:

```text
Requirements = ((Arch=="INTEL" && OpSys=="WINNTS") && Disk > DiskUsage
Rank   = (Memory > 10000) * KFlp5
```

![](img/e2283ffaea56e577ac05056b4bb738fc_341_0.png)

**Figure 14.1**
Examples of ClassAds in Condor.

## 14.2 Using Condor

The road to using Condor effectively is a short one. The basics are quickly and easily learned.

### 14.2.1 Roadmap to Using Condor

The following steps are involved in running jobs using Condor:

- **Prepare the Job to Run Job Unattended.** An application run under Condor must be able to execute as a batch job. Condor runs the program unattended and in the background. A program that runs in the background will not be able to perform interactive input and output. Condor can redirect console output (stdout and stderr) and keyboard input (stdin) to and from files. You should create any needed files that contain the proper keystrokes needed for program input. You should also make certain the program will run correctly with the files. Typically programs submitted to Condor will be console-mode programs because `stdin` and `stdout`/`err` can be redirected. However, GUI-based programs can be submitted to Condor provided they do not block waiting for mouse/keyboard input.

- **Select the Condor Universe.** Condor has five runtime environments from which to choose. Each runtime environment is called a *Universe*. Usually the Universe you choose is determined by the type of application you are asking Condor to run. There are three MPI Universes in total: one for serial jobs (Vanilla), one for parallel MPI jobs (MPI), and one for meta-schedulers (Scheduler). Section 14.2.4 provides more information on each of these Universes.

- **Create a Submit Description File.** The details of a job submission are defined in a *submit description* file. This file contains information about the job such as what executable to run, which Universe to use, the files to use for `stdin`, `stdout`, and `stderr`, requirements and preferences about the machine which should run the program, and where to send e-mail when the job completes. You can also tell Condor how many times to run a program; it is simple to run the same program multiple times with different data sets.

- **Submit the Job.** Submit the program to Condor with the `condor_submit` command.

Once a job has been submitted, Condor handles all aspects of running the job. You can subsequently monitor the job's progress with the `condor_q` and `condor_status` commands. You may use `condor_prior` to modify the order in which Condor will run your jobs. If desired, Condor can also record what is being done with your job at every stage in its lifecycle, through the use of a log file specified during submission.

When the program completes, Condor notifies the owner (by e-mail, the user-specified log file, or both) the exit status, along with various statistics including time used and I/O performed. You can remove a job from the queue at any time with `condor_rm`.

### 14.2.2 Submitting a Job

To submit a job for execution to Condor, you use the `condor_submit` command. This command takes as an argument the name of the submit description file, which contains commands and keywords to direct the queuing of jobs. In the submit description file, you define everything Condor needs to execute the job. Items such as the name of the executable to run, the initial working directory, and command-line arguments to the program all go into the submit description file. The `condor_submit` command creates a job ClassAd based on the information, and Condor schedules the job.

The contents of a submit description file can save you considerable time when you are using Condor. It is easy to submit multiple runs of a program to Condor. To run the same program 500 times on 500 different input data sets, the data files are arranged such that each run reads its own input, and each run writes its own output. Every individual run may have its own initial working directory, `stdin`, `stdout`, `stderr`, command-line arguments, and shell environment.

The following examples illustrate the flexibility of using Condor. We assume that the jobs submitted are serial jobs intended for a cluster that has a shared file system across all nodes. Therefore, all jobs use the Vanilla Universe, the simplest one for running serial jobs. The other Condor Universes are explored later.

#### Example 1

Example 1 is the simplest submit description file possible. It queues up one copy of the program `foo` for execution by Condor. A log file called `foo.log` is generated by Condor. The log file contains events pertaining to the job while it runs inside of Condor. When the job finishes, its exit conditions are noted in the log file. We recommend that you always have a log file so you know what happened to your jobs. The `queue` statement in the submit description file tells Condor to use all the information specified so far to create a job ClassAd and place the job into the queue. Lines that begin with a pound character (#) are comments and are ignored by `condor_submit`.

```text
# Example 1 ; Simple submit file
universe = vanilla
executable = foo
log = foo.log
queue
```

#### Example 2

Example 2 queues two copies of the program `mathematica`. The first copy runs in directory `run.1`, and the second runs in directory `run.2`. For both queued copies, `stdin` will be `test.data`, `stdout` will be `loop.out`, and `stderr` will be `loop.error`. Two sets of files will be written, since the files are each written to their own directories. This is a convenient way to organize data for a large group of Condor jobs.

```text
# Example 2: demonstrate use of multiple
# directories for data organization.
universe = vanilla
executable = mathematica
...
```
