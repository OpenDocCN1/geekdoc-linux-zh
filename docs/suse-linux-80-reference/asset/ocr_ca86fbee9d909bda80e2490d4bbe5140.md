+   - `status queue` — issues a status report
+   - `disable queue` — blocks new jobs from entering the queue
+   - `enable queue` — opens the queue for new jobs
+   - `stop queue` — stops the printing of jobs in the queue. The job currently being printed will be finished, however.
+   - `start queue` — resumes printing of jobs in the queue
+   - `down queue` — works like disable and stop together
+   - `up queue` — has the same affect as enable and start together
+   - `abort queue` — is the same as down, except that a job currently being printed will be stopped immediately. The jobs are retained in the queue and can continue to be processed after restarting the queue with up.

Pass these commands to `lpc` directly in the command line (e.g., `lpc status`) or run `lpc` without parameters so the dialog mode with its own prompt, `lpc>`, is started, awaiting the entry of `lpc` commands. End this dialog with `quit` or `exit`.

More information can be found in the man page for `lpc` (man lpc) and in file: `/usr/share/doc/packages/lprng/LPRng-HOWTO.html#LPRM` and in the Basics manual in Section Displaying and Managing the Queues.

> **Note**
> 
> Print jobs remain in the queues even when you shut down the computer during printing and then start Linux again. A print job that has gone wrong should be removed from the queue with the commands shown above.

# Generating Print Jobs

The `lpr` command is described in the Basics manual in Section Generating a Print Job and in the LPRng HOWTO in `file:/usr/share/doc/packages/lprng/LPRng-HOWTO.html#LPR`, so we only provide some additional information below.