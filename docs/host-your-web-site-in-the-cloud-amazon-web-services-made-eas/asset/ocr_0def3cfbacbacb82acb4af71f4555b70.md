create your own AMI. To go even further, you could have your custom AMI treat the user metadata as the URL of a script to be run when the instance starts.

# Dynamic Diagramming

In this section we'll use the EC2 APIs to retrieve the list of running instances, the EBS volumes attached to each of the instances, and the snapshots of those instances, and draw a simple system diagram. You should be able to take this program and extend it in many different ways without too much trouble.

Let's make a start. The application is going to do a lot of drawing. I sketched out my layout on a piece of graph paper and then encoded the critical sizes as PHP constants:

```
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
```

I decided to represent each running instance of EC2, the EBS volumes attached to the instance, and the snapshots for each volume as a series of connected rectangles.