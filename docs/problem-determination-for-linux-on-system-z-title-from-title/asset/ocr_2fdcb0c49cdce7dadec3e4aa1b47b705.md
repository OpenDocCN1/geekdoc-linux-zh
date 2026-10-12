Figure 5-35 shows the sample output of z/VM Performance Toolkit indicating the I/O device load and performance. The key parameters to look for are the Rate/s, Time (msec), and %Busy. The Rate/s value should not exceed the practical limit of the storage subsystem. The connect and service times in the Time (msec) column are expected to be nearly identical under normal circumstances. If the value of %Busy exceeds 50, there is a performance issue and the response time is high. For good performance, this value should be below 30.

![](bbox=[0.27, 0.28, 0.9, 0.72])

Figure 5-35 I/O load and performance check by using the z/VM Performance Toolkit

DASD statistics is a tool to monitor the activities of the DASD driver and the storage subsystem. It can be activated with the following command:

```
echo set on > /proc/dasd/statistics
```

It can be deactivated with:

```
echo set off > /proc/dasd/statistics
```