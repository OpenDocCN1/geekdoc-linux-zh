```
aws ec2 describe-availability-zones --region eu-west-1
```

The output may look something like this:

```
[{
  "AvailabilityZones": [
    {
      "State": "available",
      "RegionName": "eu-west-1",
      "Messages": [],
      "ZoneName": "eu-west-1b"
    },
    {
      "State": "available",
      "RegionName": "eu-west-1",
      "Messages": [],
      "ZoneName": "eu-west-1c"
    },
    {
      "State": "available",
      "RegionName": "eu-west-1",
      "Messages": [],
      "ZoneName": "eu-west-1d"
    }
  ]
}
```

It is worth noting that any single Spot Fleet request may not span more than one region, nor different subnets of an Availability Zone. Also, the size of the user data in a launch specification may not exceed 16 KB.

Enter the relevant information into your configuration file and then name it config.json.

# Submit your Spot Fleet request:

In the AWS command line interface, enter the command to submit your Spot Fleet request:

```
aws ec2 request-spot-fleet --spot-fleet-request-\nconfig file://config.json
```

The file config.json is the same JSON document that you created, and it specifies setup details for your Spot Fleet. You can monitor your Spot Fleet requests using:

```
aws ec2 describe-spot-fleet-requests
```

Each of your Spot Fleet requests can assume these states:

+   * submitted – Amazon is evaluating your request in preparation for launching your instances.
+   * active – once your request has been validated, this is when Amazon EC2 attempts to maintain the target number of running Spot instances in your fleet.
+   * cancelled-running – Amazon has received your request to abandon your Spot Fleet; it will not launch any additional Spot instances; currently running instances will continue to perform until they are interrupted or terminated (default).
+   * cancelled-terminating – Amazon has received your request

![](bbox=[0.45, 0.15, 0.92, 0.37])

to abandon your Spot Fleet and is in the process of forcefully terminating instances covered by this request (non-default).

* cancelled – your Spot Fleet has now been successfully cancelled, no instances are running, none will be started and Amazon will delete your request two days after the last instances were terminated.

The following will gracefully end your Spot Fleet request without terminating any of the EC2 instances that are running:

```
aws ec2 cancel-spot-fleet-requests --spot-fleet-\nrequest-ids sfr-72fbd1ce-aa42-464c-8877-\n1cee4MYFLEET--no-terminate-instances
```

If you intend to cancel your request and terminate all instances at the same time, use this command at the prompt:

```
aws ec2 cancel-spot-fleet-requests --spot-fleet-\nrequest-ids sfr-72fbd1ce-aa42-464c-8877-\n1cee4MYFLEET--terminate-instances
```

The response should look something like this (for a request without automatic instance termination):

```
{
  "SuccessfulFleetRequests": [
    {
      "SpotFleetRequestId": "sfr-72fbd1ce-aa42-464c-8877-1cee4MYFLEET",
      "CurrentSpotFleetRequestState": "cancelled_running",
      "PreviousSpotFleetRequestState": "active"
    }
  ],
  "UnsuccessfulFleetRequests": []
}
```

Spot Fleet requests exemplify how you can use cloud services on Linux in order to automate... cloud services! At any given time, you can run up to 1000 Spot Fleets per region with a total of no more than 3000 instances based on any AMIs of your choice, including Linux AMIs you may have created by yourself, possibly running custom-coded apps.

Above An Elastic Load Balancer can automatically control Auto Scaling groups as well as individual instances based on demand