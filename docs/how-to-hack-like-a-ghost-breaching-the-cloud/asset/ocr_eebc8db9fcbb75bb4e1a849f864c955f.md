Alternatively, we could opt for running a reverse shell directly in the Lambda environment, but that's far from convenient. The function runs in a minimal container where the filesystem is mounted as read-only, except for the /tmp folder, which lacks the executable flag. We would need to manually load the reverse shell in memory as an independent process, so it does not get terminated by the Lambda handler. All for what? A barren land lacking the most basic utilities that will be recycled by AWS in 60 minutes? Not worth the effort.

# Resources

+   - More information on IAM Access Analyzer: https://aws.amazon.com/iam/features/analyze-access/
- More information on CloudTrail Insights: https://amzn.to/38ROX6E
- A list of AWS S3 notification events: https://amzn.to/2MTqgIo
- More information about centralizing logs: https://www.loggly.com/ultimate-guide/centralizing-windows-logs/
- More information about querying Windows logs: https://evotec.xyz/powershell-everything-you-wanted-to-know-about-event-logs/