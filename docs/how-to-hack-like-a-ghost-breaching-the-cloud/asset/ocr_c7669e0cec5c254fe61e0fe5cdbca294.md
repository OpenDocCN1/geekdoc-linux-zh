public distribution point. We find a couple of bash scripts that automate the docker login command or provide helper functions for AWS commands, but nothing stands out as sensitive.

From this, we deduce that this bucket probably acts as a corporate-wide package distribution center. Systems and applications must use it to download software updates, packages, archives, and other widespread packages. I guess not every public S3 is an El Dorado waiting to be pilfered.

We turn to the user-data script we pulled earlier hoping for additional clues about services to query, but find nothing out of note. We even try a couple of AWS APIs with the demo role credentials to common services like EC2, Lambda, and Redshift out of desperation, only to get that delicious error message back. How frustrating it is to have valid keys yet stay stranded at the front door simply because there are a thousand keyholes to try . . . but that’s just the way it is sometimes.

As with most dead ends, the only way forward is to go backward, at least for a while. It’s not like the data we gathered so far is useless; we have database and AWS credentials that may prove useful in the future, and most of all, we gained some insight into how the company handles its infrastructure. We only need a tiny spark to ignite for the whole ranch to catch fire. We still have close to a hundred domains to check. We will get there.

# Resources

+   - See this short introduction to Burp if you are not familiar with the tool: http://bit.ly/2QEQmo9.
- Check out the progressive capture-the-flag exercises at http://flaws.cloud/ to get you acquainted with basic cloud-hacking reflexes.
- CloudBunny and fav-up are tools that can help you bust out the IP addresses of services hiding behind CDNs: https://github.com/Warflop/CloudBunny/ and https://github.com/pielco11/fav-up/.
- You can read more about techniques to uncover bucket names at the following links: http://bit.ly/36KVQn2 and http://bit.ly/39Xy6ha.
- The difference between CNAME and ALIAS records is discussed at http://bit.ly/2FBWoPU.
- This website lists a number of open S3 buckets if you’re in for a quick hunt: https://buckets.grayhatwarfare.com/.
- More information on S3 bucket policies can be found here: https://amzn.to/2Nb hngy.
- Further reading on WebSockets is available at http://bit.ly/35FsTHN.
- Check out this blog about IMDSv2: https://go.aws/35EzJgE.