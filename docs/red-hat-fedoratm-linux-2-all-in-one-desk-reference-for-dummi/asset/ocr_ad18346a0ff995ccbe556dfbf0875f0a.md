You can submit several recurring jobs with a single file. Each line with timing information about a job has a standard format with six fields — the first five specify when the job runs, and the sixth field constitutes the actual command that runs. For example, here is a line that executes the *myjob* shell script in a user’s home directory at five minutes past midnight each day:

```
5 0 * * * $HOME/myjob
```

Table 1-8 shows the meaning of the first five fields. **Note:** An asterisk (*) means all possible values for that field. Also, an entry in any of the first five fields can be a single number, a comma-separated list of numbers, a pair of numbers separated by a dash (indicating a range of numbers), or an asterisk.

+   3. Suppose the text file *jobinfo* (in the current directory) contains the job information. Submit this information to *crontab* with the following command:

```
crontab jobinfo
```

That’s it! You are set with the *cron* job. From now on, the *cron* job runs at regular intervals (as specified in the job information file), and you receive mail messages with the output from the job.

To verify that the job is indeed scheduled, type the following command:

```
crontab -l
```

The output of the *crontab -l* command shows the *cron* jobs currently installed in your name. To remove your *cron* jobs, type **crontab -r**.

**Table 1-8**
**Format for the Time of Execution in crontab Files**

| **Field Number** | **Meaning of Field** | **Acceptable Range of Values*** |
| :--- | :--- | :--- |
| 1 | Minute | 0–59 |
| 2 | Hour of the day | 0–23 |
| 3 | Day of the month | 0–31 |
| 4 | Month | 1–12 (1 means January, 2 means February, and so on) or the names of months using the first three letters (Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec) |
| 5 | Day of the week | 0–6 (0 means Sunday, 1 means Monday, and so on) or the three-letter abbreviations of weekdays (Sun, Mon, Tue, Wed, Thu, Fri, Sat) |

*An asterisk in a field means all possible values for that field. For example, if an asterisk is in the third field, the job is executed every day.*