```
```
cloudlist/create_domain.php (excerpt)
⋮
$Sdb = new AmazonSDB();

foreach (array(CL_CITY_DOMAIN,
						CL_CAT_DOMAIN,
						CL_ITEM_DOMAIN) as $domain)
{
	$Res = $Sdb->create_domain($domain);
	if (!$Res->isOk())
	{
		exit("Create domain operation failed for domain ${domain}\n");
	}
	print("Domain ${domain} created.\n");
}
⋮
```
```

Now here's a script to add a new city—actually a city/state pair:

```
```
cloudlist/add_city.php (excerpt)
#!/usr/bin/php
<?php
error_reporting(E_ALL);

require_once('cloudfusion.class.php');
require_once('include/cloudfunctions.inc.php');

if ($argc < 3)
{
	exit("Usage: " . $argv[0] . " CITY STATE\n");
}

$city  = $argv[1];
$state = $argv[2];

$key  = $state . '_' . $city;
$sattrs = array('City' => $city,
						 'State'  => $state);

$Sdb = new AmazonSDB();
```
```