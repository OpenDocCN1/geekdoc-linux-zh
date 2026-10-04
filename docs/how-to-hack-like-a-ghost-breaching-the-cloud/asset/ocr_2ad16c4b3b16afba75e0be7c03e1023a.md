processes (16 on my machine). Finally, RANDOM is a default bash variable that returns a random number on each evaluation and will be the local name of the downloaded creative. Let's see how many creatives we've nabbed:

```
root@Point1:~/creatives# ls -l |wc -l
264
```

We get 264 creatives—that's 264 hate messages, Photoshopped images, doctored videos, and carefully cut scenes emphasizing polarizing messages. Some images even discourage people from voting. Clearly, nothing is out of bounds to get the desired election outcome.

In getting these video files, we successfully completed goal number 3 from Chapter 4. We still have two crucial objectives to complete: uncovering the real identity of GP's clients and understanding the extent of the data-profiling activity.

We go back to our S3 bucket list, hoping to find clues or references to some machine learning or profiling technology (Hadoop, Spark, Flink, Yarn, BigQuery, Jupyter, and so on), but find nothing meaningful we can access.

How about another component in the delivery chain? We list all the pods running in the prod namespace looking for inspiration:

```
shell> ./kubectl get pods -n prod -o="custom-columns=\
NODE:.spec.nodeName,\
POD:.metadata.name"
```

| NODE | POD |
|---|---|
| ip-192-168-133-105.eu-... | vast-check-deployment-d34c-7qxm |
| ip-192-168-21-116.eu-... | ads-rtb-deployment-13fe-3evx |
| ip-192-168-86-120.eu-... | iab-depl-69dc-0vslf |
| ip-192-168-38-101.eu-... | cpm-factor-depl-3dbc-3qozx |
| --snip-- |  |

These pod names are as cryptic as they come. The ad business, not unlike Wall Street, has a nasty habit of hiding behind obscure acronyms that sow doubt and confusion. So, after a couple of hours of research on Wikipedia deciphering these names, we decide to focus on the ads-rtb application. RTB stands for real-time bidding, a protocol used to conduct the auction that leads to the display of a particular ad over all others on a website.

Every time a user loads a page on a website in partnership with MXR Ads, a piece of JavaScript code fires up a call to MXR Ads' supply-side platform (SSP) to run an auction. MXR Ads' SSP relays the request to other SSPs, advertising agencies, or brands to collect their bids. Each agency, acting as a demand-side platform (DSP), bids a certain amount of dollars to display their chosen ad. The amount they're willing to bid is usually based on multiple criteria: the URL of the website, the position of the ad on the page, the keywords in the page, and, most importantly, the user's data. If these criteria are suitable to the client running the ad, they'll bid higher. This auction is conducted automatically using the RTB protocol.