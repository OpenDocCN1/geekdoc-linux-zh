A health check is attached to each load balancer. The health check provides the load balancer with a target (a port, a protocol, and (for HTTP checks) a URL fragment) to be checked, along with thresholds representing the number of checks to be made before changing the state of the instance.

# Elastic Load Balancing Processing Model

The processing model is very straightforward. Here’s what you need to do:

+   1. Create an elastic load balancer by providing a reference name, an initial list of Availability Zones, the parameters for the health check, and the list of listeners. You will receive an externally visible host name in return; for example: LoadBal-79377590.us-east-1.elb.amazonaws.com. With this name in hand you can use a CNAME entry in your application’s DNS record to make the load-balanced cluster a part of your application’s web namespace.14

+   2. Add one or more EC2 instances to the load balancer using their instance IDs after ensuring that they’re prepared to respond to health checks and actual requests. The load balancer will begin to track the state (InService or OutOfService) of each instance.

+   3. Start to route traffic to the load balancer using the externally visible host name.

+   4. Add additional EC2 instances (and possibly Availability Zones) to the load balancer as traffic increases.

+   5. Delete the load balancer when you no longer need it.

As usual, all these operations can be performed using the command line tools or through the elastic load balancing API. You can also use CloudWatch to monitor the overall state of the load balancer.

The load balancer will perform health checks (or probes) on each instance under its care using the parameters that you supplied when you created it. Let’s say that a load balancer is configured with the following health check parameters (which happen to be the default values):

14 For reasons that are far too complex to explain in this footnote, you can’t use a CNAME record to define the root of your domain. You can map www.example.com to your load balancer using a CNAME, but you can’t map example.com.