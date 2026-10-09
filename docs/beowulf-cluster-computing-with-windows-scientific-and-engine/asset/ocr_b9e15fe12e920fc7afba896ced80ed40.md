running). The next section of this chapter discusses using this "job id" in various ways.

The **qsub** command has a number of options that can be specified either on the command-line or in the job script itself. Note that any command-line option will override the same option within the script file.

Table 16.1 lists the most commonly used options to **qsub**. See the PBS User Guide for the complete list and full description of the options.

| Option    | Purpose                                |
|:----------|:---------------------------------------|
| -l list   | List of resources needed by job       |
| -q queue  | Queue to submit job to                |
| -N name   | Name of job                           |
| -S shell  | Shell to execute job script           |
| -p priority | Priority value of job                  |
| -a datetime | Delay job under after datetime       |
| -j oe     | Join output and error files           |
| -h        | Place a hold on job                   |

# **Table 16.1**  
PBS commands.

The "**-l resource_list**" option is used to specify the resources needed by the job. Table 16.2 lists all the resources available to jobs running on clusters.

| Resource  | Meaning                                             |
|:----------|:----------------------------------------------------|
| arch      | System architecture needed by job                   |
| cput      | CPU time required by all processes in job           |
| file      | Maximum single file disk space requirements         |
| mem       | Total amount of RAM memory required                 |
| ncpus     | Number of CPUs (processors) required                |
| nice      | Requested "nice" (Unix priority) value              |
| nodes     | Number and/or type of nodes needed                  |
| pcpu      | Maximum per-process CPU time required               |
| pmem      | Maximum per-process memory required                 |
| wall time | Total wall-clock time needed                        |
| workingset | Total disk space requirements                     |

# **Table 16.2**  
PBS resources.