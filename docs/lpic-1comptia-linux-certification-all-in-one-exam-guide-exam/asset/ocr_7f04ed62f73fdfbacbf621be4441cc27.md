+     - lpq
+     - lprm job_number
+     - You should use a standardized process to troubleshoot printing problems.
+     - You should document the flow of print jobs to help you troubleshoot printing problems.
+     - Commonly encountered printing problems include
+       - Is the printer out of paper?
+       - Is the printer turned on?
+       - If it's a networked printer, is it connected to the network?
+       - Is the network up?
+       - Can you ping the printer from the user's workstation?
+       - Did the user select the correct printer when sending the print job?
+       - Has the correct printer driver been configured for the printer?
+     - You can use the hwclock command to manage the hardware clock.
+     - To synchronize time between networked Linux systems, you can use the nttdate command at the shell prompt.
+     - The syntax is nttdate time_server where time_server is the IP address or DNS name of another Linux system on the network that is running the time service on UDP port 37.
+     - After syncing the system time with nttdate, you may want to synchronize the system time with your hardware clock using the hwclock --systohc command.
+     - A better way to keep time synchronized on a regular schedule is to use the Network Time Protocol (NTP).
+     - NTP manages time in a much cleaner fashion than nttdate.
+     - If there is a time differential between the time provider and the time consumer (your local system) it adjusts time gradually in small increments until time is eventually synchronized.
+     - NTP is widely supported by most operating systems.
+     - A system running ntpd can function as both a time consumer and a time provider at the same time.
+     - The NTP protocol operates over IP port 123. The time consumer sends a time synchronization request to the time provider on port 123.
+     - The time provider sends its time to the consumer, and the system time on the consumer is adjusted according to the NTP algorithm.
+     - Several key NTP concepts that you need to be familiar with include the following:
+       - Stratum
+       - Stepping and slewing