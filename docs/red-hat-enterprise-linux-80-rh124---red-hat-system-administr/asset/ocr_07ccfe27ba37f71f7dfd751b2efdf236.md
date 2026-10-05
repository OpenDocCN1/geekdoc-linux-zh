```
[root@demo ~]# subscription-manager register --auto-attach
```

A valid entitlement for Red Hat Insights must be attached to the system, which you might receive as part of a Smart Management subscription. The standard Red Hat Enterprise Linux package channels must also be enabled.

2. Make sure that the insights-client package is installed on the system. In RHEL 7, this package is in the rhel-7-server-rpms channel.

```
[root@demo ~]# yum install insights-client
```

3. Use the insights-client --register command to register the system with the Red Hat Insights service and upload initial system metadata.

```
[root@demo ~]# insights-client --register
```

4. Verify that the system is active at https://access.redhat.com/insights.

![](bbox=[0.146, 0.367, 0.853, 0.636])

# # VIEWING REPORTS PROVIDED BY HAT INSIGHTS

A Red Hat Insights report shows the state of a system over time. With these reports, you can easily view current assessments of risk and identify historical trends in order to enhance decision making.

The Red Hat Insights interface provides you with information that includes:

+   * A current overall risk score based on your systems.
* Recommended actions to take on your systems, which is further broken down into categories and severities.
* Information on when systems last checked with Red Hat Insights.
* Issues that need to be prioritized based on their impact.