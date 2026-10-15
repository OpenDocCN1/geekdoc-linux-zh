# 5.2.4 z/VM shutdown workflow

When a z/VM system goes down, important steps take place. Some of them are the opposite of the IPL steps (in 5.2.1, "z/VM IPL workflow" on page 230), but are complementary. For example, saving the system attributes in the checkpoint data file. Figure 5-2 depicts the process.

![](bbox=[0.28, 0.58, 0.74, 0.82])

Figure 5-2 z/VM shutdown flowchart

From top to bottom in the z/VM shutdown flowchart, the steps are:

+   1. z/VM sends shutdown signals to guest systems (except for z/OS guests) requesting them to shut down. This allows guest system to cleanly shut themselves down before the entire system is shut off. This feature must be enabled in the SYSTEM CONFIG file (read "Starting virtual switches automatically at system startup" on page 175).
+   2. The system cleanly stops system services, such as logging and accounting.
+   3. z/VM saves the system attributes in the checkpoint data file on its RES volume.