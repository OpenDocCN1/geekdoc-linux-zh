```
```
if ($doQueue)
{
    while (true)
    {
        $message = pullMessage($sqs, FEED_QUEUE);

        if ($message != null)
        {
            $messageDetail = $message['MessageDetail'];
            $receiptHandle = (string)$message['ReceiptHandle'];

            $url = $messageDetail['FeedURL'];

            if (updateFeed($sdb, $url))
            {
                print($url . " - updated.\n");
            }
            else
            {
                print($url . " - not updated.\n");
            }

            $sqs->delete_message(FEED_QUEUE, $receiptHandle);
        }
    }
}
```
```

This code uses the `pullMessage` function that we developed for our image crawler application in Chapter 6. Again, most of the interesting work happens in `updateFeed`. Let’s take a look at it now. It’s fairly long, so we’ll examine it piece by piece.

The function starts by attempting to fetch the feed URL using the Magpie RSS parser:

```
```
function updateFeed($sdb, $url)
{
    global $stats;
    global $feedFields;
    global $itemFields;
```
```