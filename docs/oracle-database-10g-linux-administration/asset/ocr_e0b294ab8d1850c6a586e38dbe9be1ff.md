+   **I/O** As with CPU, this is a finite thing. Your system can do only so many I/Os per second. You should collect I/Os per second, reads/sec, writes/sec, read latency, write latency, and queue depth, at a minimum.

+   **Number of processes** You should always keep track of how many processes are running as a comparison.

+   **Paging** This should be monitored to determine if external factors are affecting the system performance.

+   Application Metrics

+   **Number of connections** You should monitor how many users are simultaneously connected to the web server.

+   **Pages/sec** The number of web pages per second is useful information.

+   **Requests/sec** The number of application requests per second can give you an indication on how the application layer is working.

+   **Response time** If you can collect and analyze the response times from application requests, you can determine when and if problems are occurring.

+   Database Metrics

+   **Cache hit ratio** The buffer cache hit ratio is one of the most important metrics because it tells you how efficient the buffer cache is.

+   **Shared pool hit ratio** This is similar, but on the shared pool.

+   **Wait statistics** Many Oracle database tuning experts rely on the wait statistics in order to indicate where performance bottlenecks are.

By collecting the right metrics, you can often determine where problems are, and possibly get hints on how to fix them. It is important to collect the right data in order to get the right results.

# Load Testing Tips

Here are a few tips that can be helpful when performing load testing. These are simply a random collection of dos and don'ts when performing load testing.

+   Restart the database between tests. Hit ratios and other metrics can be skewed by data left in the cache from the previous test.