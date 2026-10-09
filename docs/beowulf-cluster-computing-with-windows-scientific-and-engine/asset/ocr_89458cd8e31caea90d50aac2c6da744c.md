2. After you have verified that the resources you require exist, you can set up your batch file to request these resources. The following batch file asks for 4 nodes of the “development” resource type for 5 minutes.

```
C:\> Command Prompt\ C:\> l\>howdy.bat
ren ccs.mnodes = 4
ren ccs.account = lifka
ren ccs.minutes = 5
ren ccs.type = batch
ren ccs.requirements = @develoopment
cat MPI_COMM=TCP
hi:
cd H:\Users\Lifka
call notify lifka@tc.cornell.edu "Job started"
call mpirunscheduler
echo "TCP Run" > howdy.log
mpirun -np 8 h:\users\lifka\howdy.exe >> howdy.log
echo "WiFi Run" >>howdy.log
mpirun -np 8 h:\users\lifka\howdy.exe >> howdy.log
cclrelease
"howdy.bat": 16 lines, 426 characters.
```

3. To put your job in the queue, you must use ccssubmit, which interacts with the JobManager service on the scheduler node to queue the job for you. The JobManager returns a unique job id once the job has been successfully queued.