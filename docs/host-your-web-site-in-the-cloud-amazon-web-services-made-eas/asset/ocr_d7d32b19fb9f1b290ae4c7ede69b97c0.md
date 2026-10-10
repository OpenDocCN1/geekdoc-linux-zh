```
cloudlist/include/cloudfunctions.inc.php (excerpt)

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

```
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