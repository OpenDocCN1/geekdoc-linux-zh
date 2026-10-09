+   automountd	autofs	inoperative
+   keyserv	keyserv	inoperative
+   ypbind	yp	inoperative
+   nis_cachemgr	nisplus	inoperative
+   rpc.nisd	nisplus	inoperative
+   rpc.nispassword	nisplus	inoperative

# ## CHECKLIST

The following is a checklist for the key points in process management:

+   ❑	A process consists of an executing program and its address space. Each process is named by a positive integer number called the process identifier (PID).

+   ❑	You can set the maximum number of processes per user by using the SMIT FastPath **smitty system** and then selecting Change/Show Characteristics Of The Operating System.

+   ❑	Use the **ps** command to look at processes running on the system.

+   ❑	The nice value is an integer that represents coarse priority differences between processes. The *larger* the number, the *lower* the priority.

+   ❑	Only the superuser can improve nice priority. The nice value can be set from the command line using the **nice** command when starting a process.

+   ❑	Process owners and the superuser can modify existing process nice values by using the **renice** command.