![](bbox=[0.3, 0.09, 0.92, 0.4])

# **Tools and Locations Used in Printing**

After all required selections are complete, you will be taken back to the Hardware Configuration dialog box and all you need to do to print is to escape backward to the desktop.

So now, as you were promised, you can print the first page. The command that will accomplish this feat of modern marvels is:

```
#lpr /etc/profile (a text file that is always present)
```

Now let’s delve a bit more deeply into the details of how the printing subsystem works in Caldera OpenLinux.

The first thing to understand is that a program that runs in the background on Caldera OpenLinux handles almost all printing issues. This is the line printer daemon (LPD). Caldera offers three spooler choices. The selection of which spooler process to use was made at installation time. The most common one (and the one we will work with here) is called LPRng.

The LPD script starts the line printer daemon at boot time and can be found in the /etc/rc.d/init.d directory along with other initialization scripts. From the moment this script is executed, the lpd process runs in the background. You can find out the process number and status of this daemon with the following command:

```
#ps -ef | grep lp
```