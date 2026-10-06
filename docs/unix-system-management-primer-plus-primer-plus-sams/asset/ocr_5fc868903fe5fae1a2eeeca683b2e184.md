Chapter 4 • TESTING YOUR SYSTEMS 107

# When Your System Fails the Test

When your system fails this phase of the load test, you must determine the reason for the failure. Are the CPUs too slow? Does the system need more memory? is the database performing up to speed? Does the system need more servers? You learn how to investigate system failures and under-performance issues in Chapter 11, "Performance Tuning and Capacity Planning."

# Determining the Breaking Point

The second question we ask during a load test is "When does the system not meet the requirements?" In other words, what is the breaking point—the point at which response time or other performance parameters fall below the minimum performance specification set for your system? Judging from the Final Siege in the previous section, the bank's web server is close to the breaking point, a load of 167 concurrent connections. At that load, response time was 6.51 seconds, less than half a second under the 7-second standard for this response time.

But "close" isn't good enough for load testing. You need to determine the exact number of connections at which your system reaches the 7-second standard, the breaking point. You could test this by performing several trials, but that process would be too time-consuming. A more palatable solution is to take a few sample data points from previous runs and plot them on a graph with connections on the x-axis and response time on the y-axis. You can then tell through interpolation the approximate connection threshold by drawing a best-fit line through (or a spreadsheet do for you) the points on the graph and the 7-second value of the y-axis. If the points look more like a curve, draw the curve manually. In this example, you need more samples to increase the graph's accuracy and see an obvious pattern:

```
siege -u http://www -t 30s -d 0 -c 84
** Siege 2.09
** Preparing 84 concurrent users for battle.
The server is now under siege...
Transactions: 507 hits
Elapsed time: 30.13 secs
Data transferred: 3184467 bytes
Response time: 2.90 secs
Transaction rate: 16.83 trans/sec
Throughput: 105690.91 bytes/sec
Concurrency: 48.85
Successful transactions: 507
Failed transactions: 0
```

```
siege -u http://www -t 30s -d 0 -c 250
Transactions: 483 hits
Elapsed time: 30.38 secs
Data transferred: 3033723 bytes
Response time: 8.69 secs
Transaction rate: 15.90 trans/sec
Throughput: 99859.22 bytes/sec
```

![](bbox=[0.117, 0.903, 0.882, 0.966])