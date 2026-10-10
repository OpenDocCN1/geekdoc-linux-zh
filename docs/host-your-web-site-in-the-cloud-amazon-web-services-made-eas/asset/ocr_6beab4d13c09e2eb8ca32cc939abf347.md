So far, so good. One load balancer and a pair of instances. If one of the instances (or an instance’s entire Availability Zone) were to fail, the load balancer would notice this and route all the traffic to the other instance. Let’s make that happen!

Return to the SSH window connected to your first EC2 instance and shut down Apache:

```
<b1>: /home/webuser/helloworld/bin/stop_apache
```

Refresh your browser a couple of times, pausing for a sip of a tasty beverage perhaps,16 to allow time for the load balancer to detect that the instance is no longer passing its health check. Once this happens you’ll see the web page from the other instance.

You can confirm that the load balancer is aware that the first instance is unhealthy with the elb-describe-instance-health command:

```
$ elb-describe-instance-health LoadBal --headers
INSTANCE-ID INSTANCE-ID STATE
INSTANCE-ID i-c95650a0 InService
INSTANCE-ID i-0f414766 OutOfService
```

Now start up Apache on the first instance:

```
<b1>: /home/webuser/helloworld/bin/run_apache
```

Have another sip of your beverage and then check the instance health again:

```
$ elb-describe-instance-health LoadBal --headers
INSTANCE-ID INSTANCE-ID STATE
INSTANCE-ID i-c95650a0 InService
INSTANCE-ID i-0f414766 InService
```

Recall that the elastic load balancer uses a health check to ascertain the state of each instance. The default health check has some fairly long delays and also checks three times before deciding that an instance is unhealthy. Let’s be more aggressive: