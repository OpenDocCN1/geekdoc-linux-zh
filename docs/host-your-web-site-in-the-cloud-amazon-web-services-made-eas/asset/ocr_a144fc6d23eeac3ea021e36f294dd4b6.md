# Programming Amazon SimpleDB

In this section you’ll see how you can use CloudFusion to access all of SimpleDB’s functionality. Because CloudFusion already includes support for Amazon SimpleDB, we’ll be able to jump right into the code.

We’ll create domains and list them, then populate them with items. Then we’ll see how to deal with numeric data and run some queries. We’ll update existing items with additional data, and then delete some items and item attributes. We’ll see how to monitor domain statistics and then wrap up with a real-world example: fetching, parsing, and storing RSS feeds in SimpleDB.

I will be using three SimpleDB domains in this chapter. Here are the definitions we’ll add to **book.inc.php**:

```
```
chapter_08/include/book.inc.php (excerpt)

define('BOOK_FILE_DOMAIN', 'files');
define('BOOK_FEED_DOMAIN', 'feeds');
define('BOOK_FEED_ITEM_DOMAIN', 'feed_items');
```
```

**BOOK_FILE_DOMAIN** will be used to store information about files.

**BOOK_FEED_DOMAIN** will be used to store information about RSS feeds, and

**BOOK_FEED_ITEM_DOMAIN** will be used to store information about the items found in the RSS feeds.

You’ll need to sign up for SimpleDB² before you begin to use it. Simply visit the site and click on the **Sign Up for Amazon SimpleDB** button.