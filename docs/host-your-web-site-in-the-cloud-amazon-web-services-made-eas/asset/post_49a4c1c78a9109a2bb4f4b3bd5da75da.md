
## Chapter 11

## Putting It All Together: CloudList

In this chapter, we'll create a classified advertising application that I've named CloudList, using the Amazon EC2 infrastructure, S3, and SimpleDB. The sections of this chapter reflect my development efforts, so you should be able to see how I put the application together.

### Designing the Application

Our project is to create a simple classified advertising application. The application will allow users in a number of cities to submit and view classified ads.

We need to track the following kinds of data:

- locations—a list of cities and states
- categories—a list of classified ad categories
- items—a list of classified ads

We'll store the following fields for each ad:

- City
- State
- Date
- Price
- Category
- Title
- Description
- Image (full-sized and thumbnail)

Since each SimpleDB attribute value is limited to 1,024 bytes, we will store the descriptions, images, and thumbnails in S3. In the pursuit of simplicity we'll avoid including any contact information (email address or phone number), but feel free to extend the application yourself.

Each type of data will need its own SimpleDB domain, so let's choose some good names:

```php
// cloudlist/include/cloudfunctions.inc.php (excerpt)

define('CL_CITY_DOMAIN', 'cl_cities');
define('CL_CAT_DOMAIN', 'cl_categories');
define('CL_ITEM_DOMAIN', 'cl_items');
```

We'll put these constant definitions in the common file **cloudfunctions.inc.php**, to be included in all the CloudList application files. At this point we've yet to make any decisions about how the application will look or behave, but these considerations will have no effect on the data model.

### Utility Functions and Programs

The next step is to create some command line utility programs to populate the SimpleDB domains with initial data.

To create the SimpleDB domains we will be using, we can simply modify the *create_domain.php* script from Chapter 8:

```php
// cloudlist/create_domain.php (excerpt)
...
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
...
```

Now here's a script to add a new city—actually a city/state pair:

```php
// cloudlist/add_city.php (excerpt)
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

$sres = $Sdb->put_attributes(CL_CITY_DOMAIN, $key, $sattrs, true);

if ($sres->isOk())
{
    print("Added city ${city} in ${state}\n");
}
else
{
    $error = $sres->body->Errors->Error->Message;
    print("Could not add city: ${error}\n");
}
?>
```

We'll also need a script to add a list of one or more categories:

```php
// cloudlist/add_category.php (excerpt)
#!/usr/bin/php
<?php

error_reporting(E_ALL);

require_once('cloudfusion.class.php');
require_once('include/cloudfunctions.inc.php');

if ($argc < 2)
{
    exit("Usage: " . $argv[0] . " CATEGORY ...\n");
}

$sdb = new AmazonSDB();

for ($i = 1; $i < $argc; $i++)
{
    $category = $argv[$i];

    $Key = $category;
    $attrs = array('Category' => $category);

    $res = $sdb->put_attributes(CL_CAT_DOMAIN, $Key, $attrs, true);

    if ($res->isOk())
    {
        print("Added category ${category}\n");
    }
    else
    {
        $error = $res->body->Errors->Error->Message;
        print("Could not add category: ${error}\n");
    }
}
?>
```

Now we can use these command scripts to set up some sample data. First, we set up the domains:

```bash
$ create_domain.php
Domain cl_cities created.
Domain cl_categories created.
Domain cl_items created.
```

Then, we add some cities:

```bash
$ php add_city.php Bethesda MD
Added city Bethesda in MD
$ php add_city.php Redmond WA
Added city Redmond in WA
$ php add_city.php Boise ID
Added city Boise in ID
$ php add_city.php "San Francisco" CA
Added city San Francisco in CA
```

And then, we add the categories:

```bash
$ php add_category.php Cars Trucks Homes Furniture
Added category Cars
Added category Trucks
Added category Homes
Added category Furniture
```

If you remember from Chapter 8, each call to SimpleDB's `select` method can return up to 2,500 results, depending on the size and number of attributes returned. However, it is likely that we'll have to run SimpleDB queries that might produce long lists of results. So, let's create a function to make it easier to capture and process result sets of any size. Here's the code for the `runQuery` function:

```php
// cloudlist/include/cloudfunctions.inc.php (excerpt)

function runQuery($sdb, $query)
{
    $next = '';
    $results = array();

    do
    {
        $res = $sdb->select($query, array('NextToken' => $next));
        if (!$res->isOk())
        {
            return null;
        }

        $next = isset($res->body->SelectResult->NextToken) ?
               (string) $res->body->SelectResult->NextToken
               : '';

        foreach ($res->body->SelectResult->Item as $item)
        {
            $attributes = array();
            foreach ($item->Attribute as $attribute)
            {
                $attributes[(string) $attribute->Name] =
                       (string) $attribute->Value;
            }

            $Key = (string) $item->Name;
            $results[$Key] = $attributes;
        }
    } while ($next != '');

    return $results;
}
```

This function accepts a SimpleDB query as a string, makes a series of calls to the **select** method to retrieve all the results, and then returns a PHP associative array that contains all the results. We can then write some very simple wrappers around this function to return arrays of all cities and categories:

```php
// cloudlist/include/cloudfunctions.inc.php (excerpt)

function getCities($Sdb)
{
    $query = "select * from " . CL_CITY_DOMAIN;
    return runQuery($Sdb, $query);
}

function getCategories($Sdb)
{
    $query = "select * from " . CL_CAT_DOMAIN;
    return runQuery($Sdb, $query);
}
```

The **getCities** function returns the city data like this:

```text
Array
(
    [WA_Seattle] => Array
    (
        [State] => WA
        [City] => Seattle
    )
    [WA_Redmond] => Array
    (
        [State] => WA
        [City] => Redmond
    )
    ...
)
```

Of course, adding a new classified listing is a bit more complicated than cities and categories. It would be useful to be able to do this from the command line or from a web form. So, we will create a single (if a little complex) function named **addCloudListItem** to add a new item that can be called from the command line or a web page script.

In the **addCloudListItem** function, we'll make use of our **thumbnailImage** function from Chapter 4. Make sure you copy that function into the **cloudfunctions.inc.php** file. The **thumbnailImage** function also uses the value in the THUMB_NAIL constant to determine the thumbnail size, so we'll need to add that to our **cloudfunctions.inc.php** file as well:

```php
// cloudlist/include/cloudfunctions.inc.php (excerpt)
define( 'THUMB_SIZE', 200 );
```

We'll also reuse our uploadObject function from Chapter 4 to upload the image files to our S3 bucket, so copy that function into the cloudfunctions.inc.php file too.

Let's take the addCloudListItem code apart and examine it step by step. Here's how it begins:

```php
// cloudlist/include/cloudfunctions.inc.php (excerpt)

function addCloudListItem($sdb, $s3, $city, $state, $date,
                         $price, $category, $title, $description,
                         $imagePath)
{
```

We need a unique key since the data is destined for SimpleDB. Let's take some of the fields, put them together into a string, and then compute the MD5 hash of the string, like this:

```php
// cloudlist/include/cloudfunctions.inc.php (excerpt)
$Key = md5($city . $state . $date . $price . $category . $title);
```

The next step (and it's a big one) is to process the image associated with the listing. The $imagePath argument to the function can be a URL to a remote image or a fully qualified path name to a local one. This is made possible by the PHP function file_get_contents. If there's no image associated with the listing, we'll pass null for the argument. Here's the code we need to download the image, create a thumbnail version, and store both images in S3:

```php
// cloudlist/include/cloudfunctions.inc.php (excerpt)

if ($imagePath !== null)
{
    $imageIn  = file_get_contents($imagePath);
    $imageMem = ImageCreateFromString($imageIn);

    $fileOut = tempnam("/tmp", "_aws") . ".aws";
    $ret     = ImageJPEG($imageMem, $fileOut, 100);
    $imageOut = file_get_contents($fileOut);
```
