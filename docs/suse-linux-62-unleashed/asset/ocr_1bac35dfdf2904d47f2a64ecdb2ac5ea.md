# Networking and Internet Services
PART II

+   - The zone's refresh time is exceeded (the refresh time is the second number in the
zone data file's SOA list).

+   - The slave is listed as an NS server in the referring master or slave's zone data record,
and neither the zone in named.conf nor the options section contains a notify no
statement. The administrator changes the master's zone record, increments its serial
number (the first number in the zone data file's SOA list), and restarts named. This is
called NOTIFY.

> Note (the second event) works only with BIND 8 servers and slaves.

The point is, with only one master to maintain, you can control a large number of slave
DNS servers, making it practical to spread the work among numerous servers in different
parts of the world. Spreading the work is one advantage of slave DNS servers. A second
advantage is that it's an easy way to create a second DNS server for each zone, enhancing
reliability by through redundancy while keeping only one point of administration. Note that
though slave servers get their data from the master, they write it to disk, so they continue
to provide DNS services even if the master goes down.

In this section, you'll create a slave DNS server for the domain.cxm and 42.168.192
(reverse DNS) zones on host mtx. The following is a synopsis of how it's done:

+   1. On mtxnamed.conf, add slave zones domain.cxm and 42.168.192.in-addr.arpa.
2. Restart named on mtx.
3. On numarknamed.domain.cxm, add mtx as a second nameserver.
4. On numarknamed.192.168.42, add mtx as a second nameserver.
5. Restart named on numark.
6. 4. Test.

domain.cxm were a legitimate domain in the worldwide DNS system, both the
master and all slaves would need to be delegated authority from above before
they would work as DNS servers. However, because domain.cxm is a bogus domain
constructed for this example, it is not necessary in this case.