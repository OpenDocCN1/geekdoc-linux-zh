A reservation request can specify allocation of particular resources or a given quantity of resources. The following reservation will allocate 20 processors to users **john** and **sam** starting on April 14 at 5:00 P.M.

```
> setres -u john:sam -s 17:00_04/14 TASKS==20
```

With no duration or end time specified, this reservation will default to an infinite length and will remain in place until removed by a scheduler administrator using the **releasers** command.

Access to reservations is controlled by an access control list (ACL). Reservation access is based on job credentials, such as user or group, and job attributes, such as wall time requested. Reservation ACLs can include multiple access types and individuals. For example, a reservation might reserve resources for users A and B, jobs in class C, and jobs that request less than 30 minutes of wall time. Reservations may also overlap each other if desired, in which case access is granted only if the job meets the access policies of all active reservations.

At many sites, reservations are used on a permanent or periodic basis. In such cases, it is best to use *standing* reservations. Standing reservations allow a site to apply reservations as an ongoing part of cluster policies. The parameter **SRPERIOD** can be set to DAY, WEEK, or INFINITE to indicate the periodicity of the reservation, with additional parameters available to determine what time of the day or week the reservation should be enabled. For example, the following configuration will create a reservation named **development** that, during primetime hours, will set aside 16 nodes for exclusive use by jobs requiring less than 30 minutes.

SRPERIOD [development] DAY
SRDAYS [development] Mon Tue Wed Thu Fri
SRSTARTTIME [development] 8:00:00
SRENDTIME [development] 17:00:00
SRMAXTIME [development] 00:30:00
SRTASKCOUNT [development] 16

At times, a site may want to allow access to a set of resources only if there are no other resources available. Maui enables this conditional usage through *reservation affinity*. When specifying any reservation access list, each access value can be associated with positive, negative, or neutral affinity by using the ‘+’, ‘-’, or ‘=’ characters. If nothing is specified, positive affinity is assumed. For example, consider the following reservation line:

```
SRUSERLIST[special] bob john steve= bill-
```