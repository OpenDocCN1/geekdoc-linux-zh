To reverse the order of these jobs in `lpc`, type `topq lp 12 10 9 8`. The results are shown here:

```
```text
lpc> topq lp 12 10 9 8
lpc:
    moved cfA008simba.sampler.net.org
    moved cfA009simba.sampler.net.org
    moved cfA010simba.sampler.net.org
    moved cfA012simba.sampler.net.org
lpc> ```
```

If we look at the queue again, here's what we see:

| Rank | Owner | Job | Files | Total Size |
|:---|:---|:---|:---|:---|
| 1st | murban | 12 | schedule.txt | 6599 bytes |
| 2nd | murban | 10 | lions.txt | 1113 bytes |
| 3rd | murban | 9 | cardlist.txt | 38311 bytes |
| 4th | murban | 8 | myfile.txt | 151625 bytes |

The `topq` command can also take a username instead of a list of jobs. When `topq` is used this way, it will move all the jobs from the named user to the top of the queue.

Note that `topq` does not preempt a job that is currently running. It moves the jobs listed to the top of the queue so that they are next in line, but whatever job was printing before `topq` was used will finish printing before the job moved to the top of the queue starts. If you want a particular job to print right away, you will first have to use `lprm` to remove the job that is currently printing.

# Quitting lpc

To quit the `lpc` program, simply type either `quit` or `exit` at the `lpc>` prompt. This will put you back at the command line.

# Using lpc in Noninteractive Mode

`lpc` can also be run in noninteractive mode. In this case, simply supply the command you want to perform, along with any parameters it requires on the command line.

When `lpc` is run in noninteractive mode, it expects the first argument to be the command and anything that follows to be arguments to the command. Here's an example:

```
```bash
# lpc restart lp
lp:
    daemon (pid 2280) killed

lp:
    daemon started

# ```
```