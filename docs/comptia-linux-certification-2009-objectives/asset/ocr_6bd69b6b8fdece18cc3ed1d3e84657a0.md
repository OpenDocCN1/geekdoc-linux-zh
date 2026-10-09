# What You Do

# How You Do It

1. Cancel the jobs in the print queue.

+   a. Enter `lpq` to view the jobs in the print queue.

b. Observe that the files with job ids {job id 1} and {job id 2} are in the print queue.

c. Enter `lprm {job id 1}` to cancel the job with id {job id 1}.

d. Enter `lprm {job id 2}` to cancel the job with id {job id 2}.

e. Enter `lpq` to view the jobs in the print queue.

f. Observe that there are no jobs in the queue.

g. Minimize the **root@srvA** window.

h. Observe that two message boxes are displayed with the message "Printing of (stdin) on printer {printer name} was cancelled" for each of the canceled jobs.

i. Click **Close** two times to close both the message boxes.

j. Maximize the **root@srvA** window.

2. Add the new job to the print queue.

+   a. Enter `lpr Software_List.txt` to add the new job to the print queue.

b. Observe that the first job was only partially printed. The Software_List.txt file is printed.

c. Close the terminal window.