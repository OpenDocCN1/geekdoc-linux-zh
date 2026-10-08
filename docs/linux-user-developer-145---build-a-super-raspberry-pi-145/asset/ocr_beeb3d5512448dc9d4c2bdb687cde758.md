# Monitor a Cisco router using MRTG

Start using MRTG and its tools to monitor traffic loads

and 1.3.6.1.2.1.2.2.1.16.14, which returns the
outgoing traffic for the ADSL connection.
In the next step you will learn how to find them
for yourself.
In order to make mrtg track those two values
you may need to manually make changes to the
Target[] line of the MRTG configuration file.
The final version of the mrtg.cfg file that
supports just a Cisco router named c0wi with IP
2.86.19.123 can be found in **Fig 01**.

![](bbox=[0.06, 0.3, 0.35, 0.4])

# 13 Cisco SNMP object identifiers

Finding the correct OIDs is not always
easy, and sometimes you may need to read your
router’s documentation carefully or contact
the manufacturer. The Wi-Fi connection was
automatically found by the cfgmaker utility
but setting up the ADSL part was trickier. To
find out your own OIDs, you will need to go to
[https://www.oldview.com/mibs/O/IF-MIB.html](https://www.oldview.com/mibs/O/IF-MIB.html)
(search Google for “IF MIB download”). Next, you
should look for In and Out Octets. Then add
the desired Cisco interface number at the end
of each sequence. The available interfaces of
a Cisco device can be found by executing the
following IOS command:

```
cisco87w# show snmp mib mib index
```

The interface we wanted was called Dialer1 and
its index number was 14, but yours may vary.

![](bbox=[0.06, 0.68, 0.36, 0.8])

# 14 About Cacti

An alternative to MRTG is called Cacti.
Cacti is also an open source network graphing
application that supports plugins and utilises
RRDtool, which is a data logging and graphing
system for time series data. Cacti plugins allow
developers to generate additional Cacti features
without dealing with Cacti’s source code.

```
EnableIPv6: no
WorkDir: /srv/www/mrtg/mrtg.tsoukalos.eu/public_html
Target[c0wi1]: 1.3.6.1.2.1.2.2.1.10:481  3.6.1.2.1.2.2.1.16.14:LD2E 86.19.123:
SetEnv[c0wi1]: MRTG_INT_IP="192.168.2.1"  MRTG_INT_DESCR="ADSL"
MaxBytes[c0wi1]: 475000
Title[c0wi1]: Traffic Analysis for 14 — cisco87w.mtsouk.local
PageTop[c0wi1]: <h1>Traffic Analysis for 5 — cisco87w.mtsouk.local</h1>
<div id=\"sysdetails\">
  <table>
    <tr>
      <td>System:</td><td>cisco87w.mtsouk.local in</td>
    </tr>
    <tr>
      <td>Maintainer:</td><td>Mihalis Tsoukalos</td>
    </tr>
    <tr>
      <td>Description:</td><td>ADSL connection</td>
    </tr>
    <tr>
      <td>iType:</td><td>ADSL model</td>
    </tr>
    <tr>
      <td>iName:</td><td>Dialer</td>
    </tr>
    <tr>
      <td>Max Speed:</td><td>475.0 KBytes/s</td>
    </tr>
    <tr>
      <td>Ip:</td><td>2.86.19.123 (No DNS name)</td>
    </tr>
  </table>
</div>
```

Fig 01

> Once you see that MRTG runs
fine as a Cron job, you will not
have any other problems

![](bbox=[0.38, 0.69, 0.65, 0.91])

# 15 Final thoughts

MRTG is easy to configure but does
not support plugins. On the other hand, Cacti
is a more powerful and capable tool but, in
order to harness its full potential, you will
need to experiment with it. Cacti will be
the topic of a forthcoming article where you can
compare it with MRTG and decide which one
is better for your needs.
I strongly recommend learning both Cacti
and MRTG in order to be able to use the right
tool for the job.