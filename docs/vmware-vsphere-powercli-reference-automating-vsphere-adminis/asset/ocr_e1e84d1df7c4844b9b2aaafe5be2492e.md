# CHAPTER 16 • USING STATISTICAL DATA

Make sure you know what you are doing when changing these intervals. Changing the parameters may have a serious impact on the size of the vCenter Server database. And it could mean that you lose data—data you wanted to keep—the moment aggregation job on the SQL server fires. Remember, if you shorten the retention period of a HI, the next aggregation job will remove the data that falls outside the new retention period. Also note that you cannot specify just any value for these parameters. The accepted values are restricted; constrain VMware documentation to determine the accepted values for your vSphere version.

# Statistics Levels

The statistics level defines which metrics are available in a specific historical interval. (In the real-time interval, all metrics, except for the ones that are aggregated on the vCenter, are available.) The four statistics levels shown in Table 16.1 are

# TABLE 16.1 Statistic levels

| Level | Content |
|---|--|
| 1 | Basic metrics. Device metrics excluded. Only average rollups. |
| 2 | All metrics except those for devices. Maximum and minimum rollups excluded. |
| 3 | All metrics, maximum and minimum rollups excluded. |
| 4 | All metrics.|

You can change the statistics level through the vSphere Client.

Your first reaction may be to set all the historical intervals to level 4 with the idea "you never have enough input." But reconsider for a minute. It is really useful to know, for example, what the daily minimum and maximum memory usage was? If you do not think you have a case for this data, set the statistics level for the historical interval to level 2. This removes the data for minima and maxima during the aggregation. And most important, it will save space on your vCenter Server database, making the statistic queries faster, and making the aggregation job faster.

If you are looking to change the statistics levels from PowerCLI, you won't find a parameter on the Set-StatInterval cmdlet to do this in the current build. But with the help of the SDK method UpdatePerfInterval, it is quite easy, as shown in Listing 16.3.