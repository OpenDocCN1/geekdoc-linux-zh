And we find it’s empty. No logging. Perfect. You may be wondering why a call to this obscure API succeeded. Why would an instance profile need such a permission? To understand this weird behavior, have a look at the full list of possible S3 operations at https://docs.aws.amazon.com/. Yes, there are hundreds of operations that can be allowed or denied on a bucket.

AWS has done a spectacular job defining very fine-grained permissions for each tiny and sometimes inconsequential task. No wonder most admins simply assign wildcard permissions when setting up buckets. A user needs read-only access to a bucket? A Get* will do the job; little do they realize that a Get* implies 31 permissions on S3 alone! GetBucketPolicy to get the policy, GetBucketCORS to return CORS restrictions, GetBucketACL to get the access control list, and so forth.

Bucket policies are mostly used to grant access to foreign AWS accounts or add another layer of protection against overly permissive IAM policies granted to users. A user with an s3:* permission could therefore be rejected with a bucket policy that only allows some users or requires a specific source IP. Here we attempt to get the bucket policy for mxrads-dl to see if it does grant access to any other AWS accounts:

```
root@Point1:~# aws s3api get-bucket-policy --bucket mxrads-dl
{
  "Id": "Policy1572108106689",
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Stmt1572108105248",
      "Action": [
        "s3:List*", " s3:Get*"
      ],
      "Effect": "Allow",
      "Resource": "arn:aws:s3:::mxrads-dl",
      "Principal": { ① "AWS": "arn:aws:iam::983457354409:root" }
    }
  ]
}
```

This policy references the foreign AWS account 983457354409 ①. This account could be Gretsch Politico, an internal MXR Ads department with its own AWS account, or a developer’s personal account for that matter. We cannot know for sure, at least not yet. We’ll note it for later examination.

# Examining the Key List

We go back to downloading the bucket’s entire key list and dive into the heap, hoping to find sensitive data and get an idea of the bucket’s purpose. We have an impressive number of public binaries and .jar files. We find a collection of the major software players with different versions, such as Nginx, Java collections, and Log4j. It seems they replicated some sort of