# The legal bit

Although scraping can be a very valuable manner for getting and comparing data, its power should not be abused. If your plans are personal – such as getting bargains and rare items and keeping them to yourself – hitting the odd web page won’t even raise an eyebrow. But, if you plan to scrape many large websites for flight deals and re-publish them on the web, especially on a continual basis, you could see court action like others who have attempted such tactics.

In a nutshell, republishing scraped content on the web is a vastly different prospect to using your personal web server to find out when your item is listed below a specific price. If you look at many cases against scrapers, violation of copyright and monetary damage are often the outcome to such lawsuits.

In recent times, Amazon has cracked down on some third party providers who use scraping tools for means which it doesn’t officially approve (Ecommercebytes, http://bit.ly/bjmbJC). Since scrapers can be used to compare prices of an item on one site in order to set it at a different price on another, it is concerning that scrapers can be a controversial topic.

lines, the sim covers the bases required to extract the match each and every time.

The above match only gives us each entry that will be scraped. Now the next procedure is to get the name and price for each entry and do something with it. In order to do that, the array called $posts is iterated with a foreach loop so that the exact data for each entry is accurately kept together for analysis.

# Extending the scraper

When the array called $posts is iterated, each entry will go through the loop one at a time and taken on the name $post. Then, an array called $regex is created, since it will find the product name and price for each other entry. The next line of code creates a variable called $my_main_block which is the second string in the $post array.

Since the original scrape creates an array for each entry with the first string being the entire match and the second being only the desired text caused by the (.*?) in the first variable called $regex, we simply use it as our desired block of code.

Next, two empty arrays are made; one called $posts2 and one called $posts3. The code $posts2 = array(); makes the empty array because you want these arrays to be empty for each entry, otherwise, this won’t work. Now, another loop is used to run a check on the mother entry for its name and price. The loops run twice, we match the product name with the code:

‘preg_match_all($regex2,$my_main_block,$posts3, PREG_SET_ORDER);’

and we match the price the second time the loop runs with the code:

‘preg_match_all($regex2,$my_main_block,$posts2, PREG_SET_ORDER);’

```
if(ISSET($posts2) && !empty($posts2) && ISSET($posts3) && !empty($posts3))
```

The values are printed when an item has a name and a price. If an item is missing a name or price, it will not print. The code starting with:

provided the requirements for the sought after data. Now that you have the item and price, you can do many things. Two procedures that come to mind are to use a database to make price comparisons and the other is to send a text message – for more on this, be sure to check out the scrape-amazon-multi-match-one-page.php file on the disc.

Now that you have the code check product and price, you may want to move on to adding a third element into the equation... the product ID. When a product has a constant ID that is always used to reference the item, a name and price change is not that important, since the ID is always going to be the primary key.

With the previous example, you could easily just add that, in the same way that you would the name and price. Then, you could secretly make a second database table that reflected price changed from the original day the product was added to your Watch list.

For example, you could make a database table that inserts the item ID, name and price. Then, every day you could run a Cron job that checks for deals. A simple MySQL query could be something like:

```
SELECT NAME FROM original_table WHERE id IN
(SELECT id FROM bargains WHERE price <= '$my_price')
```

A final idea if you’re interested in taking this project further is to give yourself an email or text message when you hit the jackpot. Many phone providers these days allow you to use email to send a text message to someone’s phone. The text message is often sent via your phone number followed by an email address – such as yourphonenumber@vmbobile.ca. The PHP mail() function or SMTP can be used to send this message. Pear, for instance, has a fantastic class for sending email with SMTP.

# Scrape and Cron

Now that a scraping tutorial had been discussed, you have a basic tool set to search and scrape practically any unencrypted HTML code on the Internet.

In addition to saving some precious hard-earned dough, there are many other crafty uses where scraping can be very valuable. For example, a website owner could do a regular price comparison with their competition, in a similar way to what retail shops do but using a pen and paper, then update their ecommerce prices to always be a handy amount cheaper than the competition. Another case where gathering data can be beneficial is for research. If there are very good websites with new, updated information, you can find this information which can help further your knowledge.

Finally, you could try running a daily Cron job and look through classified ads to find extra jobs, which need your skills, or to even find a job.

```
sudo vi /etc/crontab
```

The sample text, for instance, to run a Cron job every day at 5pm would be:

```
0 17 * * * username /usr/bin/php -f /var/www/scrapers/filename.php
```

The first numbers and (*) characters set the time. Then, the appropriate username is entered followed by the path to the location of PHP on the server. Finally, the -f option and the filename explain which file is to parse and execute.

Doing things manually takes time. Why get the preferred results you are seeking through manual browsing when you can do it with automation?

![](bbox=[0.826, 0.291, 0.939, 0.425])