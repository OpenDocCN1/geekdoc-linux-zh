# ## Handling Metrics and Alerts

Now that you have a working cloud and some metrics, you will want to pass along this data to some kind of service to handle tracking and possibly billing. These services are external to OpenStack, with multiple companies and a couple open source projects, like CloudKitty, developed in the OpenStack ecosystem, offering support for the telemetry data coming from Ceilometer. Based on your needs, you'll want to research the appropriate solution for your environment. If none of the current vendors or projects meet your needs, you can write your own service that queries the API.

Once part of Ceilometer, alerts are now handled by the Telemetry Alarming service, Aodh. Like other OpenStack services, you configure alarms through the Aodh API. The alarm evaluator periodically communicates with the Ceilometer API and processes alerts through the alarm notifier, which then contacts the external systems to notify an alarm rule has been broken. This external system will be something you or your vendor creates to process the Aodh notification output.

Finally, given this data, it probably comes as no surprise that people are finding innovative ways to use this data. Utilization tracking can help a cloud operator script when they should automatically be adding resources. Problem in your infrastructure like a runaway log file or high loads? Statistics pulled from Ceilometer data can help pinpoint the instances that are struggling with disk space, CPU usage and more.

# ## Summary

With the details from this chapter, you now have the framework to start tracking metrics on a hosted compute service. With a view into it from both the Horizon dashboard and the command line and API, you can track what your system is doing through regular polling and track usage and provide information to a billing system. You can even use it for debugging using the metrics provided through Ceilometer.