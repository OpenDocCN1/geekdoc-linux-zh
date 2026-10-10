Like the code samples in the previous chapters, the programs that start with the shebang (#!/usr/bin/php) are meant to be run from the command line.

# ### Creating a Queue

Let's start by creating some queues using this code:

```
chapter_06/create_queues.php (excerpt)

#!/usr/bin/php
<?php

error_reporting(E_ALL);

require_once('cloudfusion.class.php');

if (count($argv) < 2)
{
	exit("Usage: " . $argv[0] . " QUEUE...\n");
}

$SQS = new AmazonSQS();

for ($i = 1; $i < count($argv); $i++)
{
	$Queue = $argv[$i];

	$Res = $SQS->create_queue($Queue);

	if ($Res->isOK())
	{
		print("Created queue '$queue'\n");
	}
	else
	{
		$error = (string) $Res->body->Error->Message;
		print("Could not create queue '${$queue}': $error.\n");
	}
}

exit(0);
?>
```