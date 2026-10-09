The `worker.list` tells Tomcat the number of works you want to define. The default list defines `ajp12` and `ajp13` as two workers.

Each of these workers can have its own properties set using `worker.<worker_name>.properties=value` lines. For example, in default file, the `ajp13` worker has these attributes set:

```
```
worker.ajp12.port=8007
worker.ajp12.host=localhost
worker.ajp12.type=ajp12
worker.ajp12.lbfactor=1
```
```

The first line sets the port number, which is used by the `ajp12` worker to listen for requests. The second line defines the hostname where this worker is listening for connections. The third line defines the type of the worker. I think it was a poor choice to name the worker `ajp12` when it is also type `ajp12`. You can name a worker anything you want as long as the name consists of letters and numbers. The fourth line gives the worker a weight rating for load-balancing purposes. A high number indicates a powerful machine and when there are multiple machines involved in a load-balanced scenario, the load-balancer worker will choose the worker, which has the highest lbfactor first.

The same properties for the `ajp13` worker are defined in the next four lines in the `workers.properties` file.

The next two lines define a worker called `loadbalancer`, which is of type `lb` and which balances workers `ajp12` and `ajp13` using a round-robin schema. These two lines are:

```
```
worker.loadbalancer.type=lb
worker.loadbalancer.balanced_workers=ajp12, ajp13
```
```

The next two lines define a worker called `inprocess` of type `jni`. This worker's `class_path` is defined by setting the second line to `/var/tomcat/classes` for a Linux system:

```
```
worker.inprocess.type=ini
worker.inprocess.class_path=${workers.tomcat_home}${ps}${ps}classes
```
```

The next six lines add six library files to the class path:

```
```
worker.inprocess.class_path=${workers.tomcat_home}${ps}lib${ps}jaxp.jar
worker.inprocess.class_path=${workers.tomcat_home}${ps}lib${ps}parser.jar
worker.inprocess.class_path=${workers.tomcat_home}${ps}lib${ps}jars.jar
worker.inprocess.class_path=${workers.tomcat_home}${ps}lib${ps}servlet.jar
worker.inprocess.class_path=${workers.tomcat_home}${ps}lib${ps}webserver.jar
worker.inprocess.class_path=${workers.java_home}${ps}lib${ps}tools.jar
```
```