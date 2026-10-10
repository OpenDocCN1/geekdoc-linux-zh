object like the previous scripts, and the `list_distributions` method to retrieve the details of the distributions.

The response object can be queried in the same way as our previous S3 scripts. In the response returned to the `list_distributions` method, the `$res->body->DistributionSummary` property will contain an array of `SimpleXMLElement` objects, one for each CloudFront distribution. The script above simply iterates over this array and extracts the Id, DomainName, and Origin property of each for display in the output, formatted into a table similar to the following:

![](bbox=[0.12, 0.3, 0.85, 0.42])

When you run this script with your AWS account, the Id and Domain Name columns will show you unique values.

# ## Listing S3 Files with Thumbnails

Okay, time for the last script in this chapter! We first need one more utility function to make this work: the findDistributionForBucket function that will return the CloudFront distribution for a given S3 bucket. You guessed it, we'll put this one in our book.inc.php file:

```
<!-- chapter_04/include/book.inc.php (excerpt) -->
function findDistributionForBucket($cf, $bucket)
{

    $res = $cf->list_distributions();

    if (!$res->isOK())
    {
        return null;
    }

    $needle = $bucket . ".";
    $distributions = $res->body->DistributionSummary;
```