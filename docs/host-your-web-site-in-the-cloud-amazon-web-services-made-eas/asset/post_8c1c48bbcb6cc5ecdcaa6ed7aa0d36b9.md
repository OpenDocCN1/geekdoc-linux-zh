
```
<dev>: rm -/.bash_history
rm: remove regular file `/root/.bash_history'? y
<dev>: cd /var/log
<dev>: > cron
<dev>: > maillog
<dev>: > secure
<dev>: > spooler
<dev>: > yum.log
<dev>: > httpd/error_log
<dev>: > httpd/access_log
```

## Image Creation

The next step is to upload the bundle to Amazon S3. To do this you'll need your AWS access key ID, your secret access key, and an available S3 bucket.

After you have scrubbed your root file system, you can create an image by right-clicking on the instance in the AWS Management Console and choosing the option labeled Create Image (EBS AMI). The Create Image dialog will be displayed, as shown in Figure 5.22.

![](img/4a5ba0dd041e08e6a67fa31d52309995_162_0.png)

Give your instance a name and a description, and click the **Create This Image** button. Your instance will be rebooted as part of the image creation process, so don't be alarmed when you lose touch with it. The time that the image creation process takes is proportional to the size of your instance's root file system. The instance's state will be displayed as **available** during the creation process, but you won't be able to log in until the process has concluded.

### Reusing and Sharing the AMI

Now that you've created your AMI, you can use the **My AMIs** tab of the **Launch Instance Wizard** to find and launch instances of it. Until you give the say-so, you're the only one with permission to do this; the AMI's visibility is set to **Private**.

You can choose to share your new AMI with selected AWS users or with the entire AWS community. If you elect to share with selected users you'll need their AWS account numbers.

Right-click on your AMI in the console's **AMIs** view, then choose the **Edit Permissions** option to launch the dialog shown in Figure 5.23.

![](img/4a5ba0dd041e08e6a67fa31d52309995_163_0.png)

Under **Add Launch Permission**, enter the account number of a particular AWS user to share it with them. Click the **add additional user** link each time you need to enter another account number. You can select **Public** to share the AMI with the entire AWS community.

## Using the EC2 API

Key to the concept of the programmable data center is the fact that every resource can be manipulated by an external program. In this section we’ll take a look at a program that does exactly that. In just over 100 lines (including comments and error checking) the program does the following:

- launches an EC2 instance
- waits for the instance to transition to the “running” state
- allocates a public IP address
- attaches the IP address to the EC2 instance
- allocates a pair of 1GB EBS volumes
- attaches the volumes to the EC2 instance

The program starts out in the usual way:

```php
#!/usr/bin/php
<?php
error_reporting(E_ALL);

require_once('cloudfusion.class.php');
require_once('include/book.inc.php');

$ec2 = new AmazonEC2();
```

Like the S3 and CloudFront access objects that we used in Chapter 4, the EC2 access object provides a complete set of methods for access to the EC2 functionality.

Launching an instance is a lot easier than buying and installing new hardware:

```php
$Options = array('KeyName' => “Jeff’s Keys”,
                 'InstanceType' => “m1.small”);

$Res = $ec2->run_instances(“ami-48aa4921”, 1, 1, $Options);
```

if (!$res->isOK())
{
    exit("Could not launch instance: "
        . $res->body->Errors->Error->Message . "\n");
}

After forming an options array to specify the key pair and desired instance type, this code simply calls the run_instances method and checks for errors.

We'll need the instance ID and the instance's Availability Zone, so let's fetch and print them:

$instances     = $res->body->instancesSet;
$instanceId    = (string)$instances->item->instanceId;
$availabilityZone = (string)$instances->item->placement->
                     availabilityZone;

print("Launched instance ${instanceId} "
      ."in availability zone ${availabilityZone}.\n");

The next step is to poll the instance state every ten seconds until it's actually up and running. EC2 services will stop an EBS volume from being attached to an instance while the instance is still in the process of booting up. A simple loop does the trick:

do
{
    $options = array('InstanceId.1' => $instanceId);
    $res     = $ec2->describe_instances($options);
    $instances = $res->body->reservationSet->item->instancesSet;
    $state   = $instances->item->instanceState->name;
    $running = ($state == 'running');

    if (!$running)
    {
        print("Instance is currently in "
              ."state ${state}, waiting 10 seconds\n");
        sleep(10);
    }
}
while (!$running);

The `describe_instances` method returns the state of the instance passed in via the `$options` array. The actual instance state is deeply nested within the returned result, so a pair of statements are used to fetch it. The loop iterates until the instance state is the string "running".

Okay, now we need an Elastic IP address. Let's allocate it and display it like this:

$res = $ec2->allocate_address();
if (!$res->isOK())
{
    exit("Could not allocate public IP address.\n");
}

$publicIP = (string)$res->body->publicIp;
print("Assigned IP address $publicIP.\n");

The `allocate_address` method does the heavy lifting, and the assigned address is extracted from the returned result in the usual way.

With the address in hand it's time to attach it to the instance, like so:

$res = $ec2->associate_address($instanceId, $publicIP);
if (!$res->isOK())
{
    exit("Could not associate IP address $publicIP " .
         "with instance $instanceId.\n");
}

print("Associated IP address $publicIP " .
      "with instance $instanceId.\n");

So far, so good! Now we can create a pair of 1GB EBS volumes and display their IDs:

$res1 = $ec2->create_volume(1, $availabilityZone);
$res2 = $ec2->create_volume(1, $availabilityZone);

if (!($res1->isOk() || !$res2->isOk()))
{
    exit("Could not create EBS volumes.\n");
}

$volumeId1 = (string)$res1->body->volumeId;
$volumeId2 = (string)$res2->body->volumeId;

print("Created EBS volumes ${volumeId1} and ${volumeId2}.\n");

Notice that the volumes are created in the instance’s Availability Zone, as is required.

The final step is to attach the volumes to the instance, and that’s fairly easy using the attach_volume method:

$res1 = $ec2->attach_volume($volumeId1, $instanceId, '/dev/sdf');
$res2 = $ec2->attach_volume($volumeId2, $instanceId, '/dev/sdg');

if (!($res1->isOk() || !$res2->isOk()))
{
    exit("Could not attach EBS volumes " .
         "${volumeId1} and ${volumeId2} " .
         "to instance ${instanceId}.\n");
}

print("Attached EBS volumes ${volumeId1} and ${volumeId2} " .
      "to instance ${instanceId}.\n");
?>

And there you have it. We just instantiated a Linux server with an Elastic IP address and a pair of disk volumes attached, with just eight calls to the EC2 API.

## Closing Thoughts

We've learned a lot in this chapter. We've learned about persistent and ephemeral EC2 resources, security groups, and the EC2 pricing model. We then prepared our keys and launched our very first EC2 instance. We gave it a public IP address and created an EBS volume, then verified that the Apache web server was running as expected. From there we downloaded and installed CloudFusion and ran a test script. We learned all about AMIs—where to find them, how to choose them, and how to create them from scratch. Along the way we became familiar with many aspects of the AWS Management Console, and we learned how to allocate and manipulate EC2 resources using the actual EC2 APIs.

Before wrapping up this chapter I would like to leave you with a few closing thoughts.

The ease with which you can start, configure, and terminate instances should make you start to think about them in a different way. Instead of looking at your server as a one-off, very precious piece of hardware, you can see it as an expandable, temporary resource. If you need a second server to test a new version of your code, just go ahead and launch it. If you want to see how your code performs with a different Linux distribution or with a newer version of MySQL, again, just go ahead and launch an instance.

I'm fairly sure that you'll have gained an appreciation for the richness and power embodied in the AWS Management Console. As you saw in the code sample presented at the end of this chapter, all this power is available through the EC2 APIs as well.
