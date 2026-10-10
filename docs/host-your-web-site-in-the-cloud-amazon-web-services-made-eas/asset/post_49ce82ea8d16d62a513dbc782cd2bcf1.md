
<dev>: wget -q http://169.254.169.254/latest/meta-data/instance-id
<dev>: wget -q http://169.254.169.254/latest/meta-data/public-ipv4
<dev>: wget -q http://169.254.169.254/latest/meta-data/placement/availability-zone

Note that these requests (and all other requests for instance metadata) must be made from within the instance itself. Here is the resulting metadata:

<dev>: cat public-ipv4
174.129.84.219
<dev>: cat instance-id
i-d830dfb0
<dev>: cat availability-zone
us-east-1b

You can also supply your own metadata when you launch an EC2 instance. This data is called user data. The AWS Management Console, the ElasticFox tool, and the ec2-run-instances command line tool each provide a way to specify this data. The AWS Management Console supports this function as an advanced option, as shown in Figure 10.4.

![](img/4a5ba0dd041e08e6a67fa31d52309995_343_0.png)

Figure 10.4. Launch an EC2 instance with user data

In this example, “Role=Server,Size=Small,Name=MainServer,Input=Queue1” is the string contained in my user data. I can retrieve this information immediately after my instance has launched, and use it to control the behavior of my instance.

Once launched, the user data can be retrieved like this:

<dev> wget -q http://169.254.169.254/latest/user-data
<dev> cat user-data
Role=Server,Size=Small,Name=MainServer,Input=Queue1

Of course, we can also retrieve and process the user metadata using a simple PHP program:

chapter_10/ec2_user_data.php (excerpt)

#!/usr/bin/php
<?php

$userData = file_get_contents(
        'http://169.254.169.254/latest/user-data');
$options = array();

foreach (explode(",", $userData) as $userDataItem)
{
    if (preg_match("!^([a-zA-Z]{1,})=([a-zA-Z0-9]{1,})$!",
            $userDataItem, $parts))
    {
        $name  = $parts[1];
        $value = $parts[2];

        $options[$name] = $value;
    }
}

print_r($options);
?>

The file_get_contents function fetches the user metadata. The string is broken up at comma boundaries using PHP’s explode function, producing name-value pairs in the form Role=Server.

You can use the user metadata facility any way you’d like. You can pass server names, server roles, SQS queue names, sizes, limits, and so forth. You’ll need to create your own AMI. To go even further, you could have your custom AMI treat the user metadata as the URL of a script to be run when the instance starts.

# Dynamic Diagramming

In this section we'll use the EC2 APIs to retrieve the list of running instances, the EBS volumes attached to each of the instances, and the snapshots of those instances, and draw a simple system diagram. You should be able to take this program and extend it in many different ways without too much trouble.

Let's make a start. The application is going to do a lot of drawing. I sketched out my layout on a piece of graph paper and then encoded the critical sizes as PHP constants:

chapter_10/ec2_diagram.php (excerpt)

#!/usr/bin/php
<?php

error_reporting(E_ALL);
require_once('cloudfusion.class.php');
require_once('include/book.inc.php');

// Define shape geometry
define('LEFT_MARGIN', 16);
define('RIGHT_MARGIN', 16);
define('TOP_MARGIN', 16);
define('BOTTOM_MARGIN', 16);
define('TEXT_MARGIN', 4);
define('TEXT_LINE_HEIGHT', 14);
define('INSTANCE_WIDTH', 128);
define('INSTANCE_HEIGHT', 64);
define('VOLUME_WIDTH', 96);
define('VOLUME_HEIGHT', 64);
define('SNAP_WIDTH', 96);
define('SNAP_HEIGHT', 64);
define('VOLUME_GAP', 16);
define('SNAP_GAP', 16);

I decided to represent each running instance of EC2, the EBS volumes attached to the instance, and the snapshots for each volume as a series of connected rectangles.

I stacked the instances vertically, the volumes in a horizontal row, and the snapshots in a vertical column. Figure 10.5 shows a cleaned-up version of my sketch.

![](img/4a5ba0dd041e08e6a67fa31d52309995_346_0.png)

Each instance and its attached parts occupies a rectangular space on the final image, with a surrounding margin represented by LEFT_MARGIN, RIGHT_MARGIN, TOP_MARGIN, and BOTTOM_MARGIN. The instances, volumes, and snapshots are drawn as rectangles of size INSTANCE_WIDTH by INSTANCE_HEIGHT, VOLUME_WIDTH by VOLUME_HEIGHT, and SNAP_WIDTH by SNAP_HEIGHT, respectively. TEXT_MARGIN allows for some space between the edge of each rectangle and the text inside, and TEXT_LINE_HEIGHT is the space between lines of text. VOLUME_GAP is the horizontal space between volume rectangles and SNAP_GAP is the vertical space between snapshot rectangles.

As always, we need to create the objects that let us access EC2 and S3:

chapter_10/ec2_diagram.php (excerpt)
$ec2 = new AmazonEC2();
$s3 = new AmazonS3();

Next we fetch the list of EC2 instances, EBS volumes, and EBS volume snapshots like this:

chapter_10/ec2_diagram.php (excerpt)
$resInstances = $ec2->describe_instances();
$resVolumes = $ec2->describe_volumes();
$resSnapshots = $ec2->describe_snapshots();

This tiny code fragment retrieves all the important information about our system configuration. It never hurts to check for errors before proceeding, so let's do that now:

chapter_10/ec2_diagram.php (excerpt)
if (!$resInstances->isOk() ||
    !$resVolumes->isOk() ||
    !$resSnapshots->isOk())
{
    exit("Error retrieving system information.");
}

Unlike most of the other (and much simpler) programs in this book, I'm taking an object oriented approach here. I created classes to represent EC2 Regions, instances, volumes, and snapshots. Each class contains references to the objects that it logically owns or contains:

- Regions contain instances
- instances contain volumes
- volumes contain snapshots

I chose to omit storing information about volumes that are unattached to instances or snapshots for non-existent volumes (which are perfectly legitimate situations).

The Region is the top-level object, so it's created first:

chapter_10/ec2_diagram.php (excerpt)
$Region = new Region('us-east-1');

Next we can iterate through the list of instances, gathering the interesting attributes for each instance, using them to create an Instance object, and then adding the new object to the Region. Here's how to do that:

chapters/10/ec2_diagram.php (excerpt)

foreach ($resInstances->body->reservationSet->item as $itemSet)
{
    foreach ($itemSet->instancesSet->item as $item)
    {
        $instanceId        = (string) $item->instanceId;
        $state             = (string) $item->instanceState->name;
        $instanceType      = (string) $item->instanceType;
        $availabilityZone  = (string) $item->placement->availabilityZone;

        if ($state != 'terminated')
        {
            $Region->AddInstance(new Instance($availabilityZone,
                $instanceId,
                $state,
                $instanceType));
        }
    }
}

The code skips instances in the terminated state since they've been shut down.

Next, we can do the same sort of processing for each EBS volume:

chapters/10/ec2_diagram.php (excerpt)

foreach ($resVolumes->body->volumeSet->item as $item)
{
    $volumeId        = (string) $item->volumeId;
    $size            = (string) $item->size;
    $availabilityZone = (string) $item->availabilityZone;

    if ($item->attachmentSet->item)
    {
        $instanceId = (string) $item->attachmentSet->item->instanceId;
        $device     = (string) $item->attachmentSet->item->device;

        $Region->AddVolume(new Volume($availabilityZone,
            $volumeId,
            $instanceId,
            $size,
            $device));
    }
}

And the same for each snapshot:

chapter_10/ec2_diagram.php (excerpt)

foreach ($resSnapshots->body->snapshotSet->item as $item)
{
    $snapshotId = (string) $item->snapshotId;
    $volumeId   = (string) $item->volumeId;
    $startTime  = (string) $item->startTime;

    $Region->AddSnapshot(new Snapshot($snapshotId,
        $volumeId,
        $startTime));
}

At this point the data structure is built. If you want to see what it looks like for yourself, dump it out like this:

print_r($Region);

My Region class has a Draw method. This method uses the GD library to render the instances, volumes, and snapshots to an in-memory image and then returns it:

chapter_10/ec2_diagram.php (excerpt)

$image = $Region->Draw();

The final step is to write the in-memory image to the file system in GIF format, read the GIF into memory, and then store it in Amazon S3:

chapter_10/ec2_diagram.php (excerpt)

$imageOut = tempnam("/tmp", "aws") . ".gif";
ImageGIF($image, $imageOut);

$imageOutBits = file_get_contents($imageOut);
