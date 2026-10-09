Determine a goal for your server. Make an estimate (or guess) of how many requests you want to be able to service from your Web server. Write it down in a goal statement such as, “I wish to service $N$ requests per second.”

Restart your Web server and from a system other than the Web server, run the ab command as follows:

```
```
./ab -n number_of_total_requests \
   -c number_of_simultaneous_requests \
      http://your_web_server/page
```
```

For example:

```
```
./ab -n 1000 -c 50 http://www.domain.com/
```
```

The ApacheBench tool will make 50 concurrent requests and a total of 1,000 requests. Sample output is shown below:

```
```
Server Software:        Apache/2.0.16
Server Hostname:        localhost
Server Port:            80

Document Path:          /
Document Length:        1311 bytes

Concurrency Level:      50
Time taken for tests:   8.794 seconds
Complete requests:      1000
Failed requests:        0
Total transferred:      1754000 bytes
HTML transferred:       1311000 bytes
Requests per second:    113.71
Transfer rate:          199.45 kb/s received

Connection Times (ms)
              min     avg     max
Connect:        0      0       5
Processing:   111   427     550
Total:        111   427     555
```
```

Notice that Requests per second is 113.71 for accessing the home page of the http://www.domain.com site. Change the concurrent request count to a higher number and see how the server handles additional concurrent load.

Now change the values for the MaxClients, ThreadsPerChild, MaxThreadsPerChild, and so on based on your MPM, restart Apache, and apply the same benchmark tests by using ab as before. You should see your Requests per second go up and down based on numbers you try. As you tweak the numbers by changing the directive values, make sure you record the values and the performance so that you can determine what is a good setting for you.