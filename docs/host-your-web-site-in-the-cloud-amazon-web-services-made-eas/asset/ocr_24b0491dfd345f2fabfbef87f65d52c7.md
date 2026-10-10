We'll store the following fields for each ad:

+   - City
+   - State
+   - Date
+   - Price
+   - Category
+   - Title
+   - Description
+   - Image (full-sized and thumbnail)

Since each SimpleDB attribute value is limited to 1,024 bytes, we will store the descriptions, images, and thumbnails in S3. In the pursuit of simplicity we'll avoid including any contact information (email address or phone number), but feel free to extend the application yourself.

Each type of data will need its own SimpleDB domain, so let's choose some good names:

```
cloudlist/include/cloudfunctions.inc.php (excerpt)

define('CL_CITY_DOMAIN', 'cl_cities');
define('CL_CAT_DOMAIN', 'cl_categories');
define('CL_ITEM_DOMAIN', 'cl_items');
```

We'll put these constant definitions in the common file **cloudfunctions.inc.php**, to be included in all the CloudList application files. At this point we've yet to make any decisions about how the application will look or behave, but these considerations will have no effect on the data model.

# ## Utility Functions and Programs

The next step is to create some command line utility programs to populate the SimpleDB domains with initial data.

To create the SimpleDB domains we will be using, we can simply modify the *create_domain.php* script from Chapter 8: