![](bbox=[0.14, 0.14, 0.23, 0.21])

Even more verbose checkpoint information will also be recorded in the Alert log when the LOG_CHECKPOINTS_TO_ALERT is set to TRUE in the init.ora.

# Using Performance Manager to Measure Checkpoint Performance

The Performance Manager component of OEM can also be used to monitor the performance of checkpoint activity. The Average Dirty Queue Length option of the Performance Manager I/O feature indicates how often checkpoint activity is occurring. Figure 7.9 shows the GUI output from a sample Average Dirty Queue Length screen.

![](bbox=[0.12, 0.43, 0.71, 0.45])

![](bbox=[0.31, 0.46, 0.83, 0.74])

The output in Figure 7.9 shows that the Average Dirty Queue Length was close to zero throughout the monitoring period. This indicates that checkpoint activity occurred fairly frequently during the monitoring period. High or steadily increasing values for Average Dirty Queue Length indicate a potential checkpoint-related performance bottleneck.

# Improving Checkpoint Performance

As described in the previous section, the checkpoint event is an I/O intensive moment in the database. Once a checkpoint is started, you would like it to complete successfully. If it does not, the checkpoint event ends up causing unnecessary I/O by prompting DBW0 and LGWR to empty the Database