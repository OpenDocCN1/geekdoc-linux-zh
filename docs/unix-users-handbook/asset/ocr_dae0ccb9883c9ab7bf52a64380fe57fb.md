We could have mapped this network drive at the command line on the PC using **net use E:\\192.168.1.1\\root**. After having successfully mapped **E:** to **/** on **linux1** using *explorer*, we can access this directory on our Windows system.

![](bbox=[0.04, 0.26, 0.9, 0.55])

**Figure 20-5   View E:\\etc on Windows System**

In Figure 20-5, we have changed to the **/etc** directory on **linux1** and have selected the **smb.conf** file. You can see from this example that **/** on **linux1** is fully accessible on the Windows system. We have access to all three shares on **linux1**, as the following listing shows on the Windows system: