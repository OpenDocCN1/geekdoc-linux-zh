
Here’s some code to illustrate how you can use CloudFusion to create an S3 bucket. I’m including this code to show you that CloudFusion is clean and easy to use:

```php
#!/usr/bin/php
<?php
    error_reporting(E_ALL);
    require_once('cloudfusion.class.php');

    $S3 = new AmazonS3();
    $res = $S3->create_bucket('jeff_barr_bucket');

    if ($res->isOK())
    {
        print("Bucket created\n");
    }
    else
    {
        print("Error creating bucket\n");
    }
?>
```

First, we create a new AmazonS3 object from which we can access the functions we need. Creating a bucket involves a single method call to the `create_bucket` function, supplying the new bucket’s name. We can then test to ensure that there were no errors by using the `isOK` method.

No need to worry about the details right now—we’ll be jumping in before too long. The CloudFusion project maintains a GitHub repository^13 and a web site.^14 We’ll dive deeper into CloudFusion in the section called “Installing CloudFusion” at the end of this chapter, so it’s unnecessary to download or configure it just yet.

## Command Line Tools

Not so long ago, typing commands into a shell window was considered the state of the art in human-computer interaction. Although visual tools have obviated much of the need to do this on a routine basis, there are still a good number of reasons to use the command line from time to time. Command line tools are easier to use as part of a script. Routine operations that involve a sequence of commands and some decision-making can be automated. The output from two or more command line tools can be blended together. All things considered, these tools still serve a purpose.

Amazon supplies a number of command line tools. The first set is called API tools because there's one tool for each function in the EC2 API. For example, the `ec2-run-instances` command is a wrapper around the EC2 RunInstances function. The tools are written in Java; the source, however, is unavailable. The EC2 API tools are divided into four packages:

- The Amazon EC2 API Tools[^15] provide access to the core EC2 API functions.
- The Amazon CloudWatch API Tools[^16] provide access to the CloudWatch API functions.
- The Auto Scaling API Tools[^17] provide access to the Auto Scaling API functions.
- The Elastic Load Balancing API Tools[^18] provide access to the Elastic Load Balancing API functions.

Amazon also supplies a set of AMI tools.[^19] More special-purpose in nature, you use these tools to create, upload, and register customized Amazon Machine Images (AMIs).

Members of the AWS developer community have created a number of command line tools. Some of these focus on providing access to a single service; others aim to be all-encompassing. A good example of the latter is Tim Kay's top-rated `aws` command.[^20] This aspiring Swiss Army Knife now provides functions for EC2 services, S3, and SQS. Written in Perl, this script runs on Linux and Windows.

## Visual Tools

At the top of the stack we find the visual tools. Developers have really exercised their creativity in this area and there are many tools to choose from; I'll cover a few of my favorites here. There are at least four types of tools:

- Dynamic Ajax-powered applications—the AWS Management Console is a good example of this type of application.
- Browser extensions—the ElasticFox and the S3fox are both extensions to the Firefox web browser.
- Standalone desktop applications—CloudBerry Explorer, Bucket Explorer, and the SimpleDB Explorer are all in this category.
- Device-specific applications—the iPhone applications from Ylastic and Direct Thought are both in this category.

### AWS Management Console

The AWS Management Console[^21] is effectively part of AWS. Because it's part of the AWS site, there's no configuration work required. Once you've logged in, you have full access to all EC2 services, CloudFront, and Elastic MapReduce. You can see your running instances and launch new ones. You can manage security groups, Elastic Block Store volumes, Elastic IP addresses, and identity key pairs. Figure 3.1 shows what it looks like.

![](img/4a5ba0dd041e08e6a67fa31d52309995_70_0.png)

**Figure 3.1. The AWS Management Console**

### ElasticFox

ElasticFox[^22] is a Firefox extension available for free. After installing the extension and restarting your browser, you can access ElasticFox through the **Tools** menu. ElasticFox is an open source tool and has a SourceForge project of its very own.

Figure 3.2 shows ElasticFox listing available AMIs.

![](img/4a5ba0dd041e08e6a67fa31d52309995_71_0.png)

**Figure 3.2. Elasticfox displaying a list of available AMIs**

### S3Fox

S3Fox[^23] is a free S3 and CloudFront extension for Firefox, and a product of Suchi Software Solutions. This too makes it easy to copy files from your desktop to Amazon S3 (and vice versa) using a two-paned interface. Figure 3.3 shows what the S3Fox looks like; the local disk is in the left pane, while the S3 bucket is on the right.

![](img/4a5ba0dd041e08e6a67fa31d52309995_72_0.png)

**Figure 3.3. The S3Fox Organizer with its dual-paned approach**

### CloudBerry Explorer

CloudBerry Explorer[^24] is a free, standalone desktop application and a product of CloudBerry Lab. You can manage your S3 buckets, copy files into and out of Amazon S3, and create CloudFront distributions. There’s also a professional version that supports file encryption, data compression, and access to FTP servers. A screenshot from the free version is shown in Figure 3.4.

![](img/4a5ba0dd041e08e6a67fa31d52309995_73_0.png)

### Bucket Explorer

Bucket Explorer[^25] is a commercial desktop application from Chambal.com. You can download free trial versions for Windows, Mac, and Linux. In addition to managing S3 buckets and objects, Bucket Explorer supports shared buckets, local and remote synchronization, and versioning. Figure 3.5 shows a screenshot of Bucket Explorer in action.

![](img/4a5ba0dd041e08e6a67fa31d52309995_74_0.png)

**Figure 3.5. Bucket Explorer with a bucket list on top and contents at the bottom**

### SimpleDB Explorer

SimpleDB Explorer,[^26] shown in Figure 3.6, is also produced by Chambal.com and is available in versions for Windows, Mac, and Linux. It features complete read-write access to SimpleDB domains and metadata, along with querying, sorting, and pagination through large result sets.

![](img/4a5ba0dd041e08e6a67fa31d52309995_75_0.png)

**Figure 3.6. The SimpleDB Explorer interface**

### Ylastic

Ylastic[^27] supports complete management of EC2 services, SQS, S3, CloudFront, and SimpleDB on Apple iPhone and phones based on the Google Android operating system (the latter can be seen in Figure 3.7). While it’s advisable to use a more capable device as your primary AWS management tool, it can certainly be useful to have a portable management tool at hand.

![](img/4a5ba0dd041e08e6a67fa31d52309995_76_0.png)

### DirectEC2

The Direct Thought company has created DirectEC2,[^28] a native interface to EC2 services for the iPhone and the iPod Touch. The application features complete control of each aspect of EC2 functionality: AMIs, running instances, EBS volumes, EBS volume snapshots, Security Groups, IP addresses, and Keypairs. Figure 3.8 demonstrates what it looks like.

![](img/4a5ba0dd041e08e6a67fa31d52309995_77_0.png)

## Creating an AWS Account

You're going to need an AWS account in order to run the code in this book. The accounts are free and you'll only be charged for the services that you actually use, but you'll need an email address and credit card in order to create your account.

You can skip this section if you already have an active AWS account.

[^15]: http://developer.amazonaws.com/connect/entry.jsp?externalID=351&categoryID=251
[^16]: http://developer.amazonaws.com/connect/entry.jsp?externalID=253&categoryID=251
[^17]: http://developer.amazonaws.com/connect/entry.jsp?externalID=253&categoryID=251
[^18]: http://developer.amazonaws.com/connect/entry.jsp?externalID=368
[^19]: http://developer.amazonaws.com/connect/entry.jsp?externalID=368
[^20]: http://timkay.com/aws/
[^21]: http://console.aws.amazon.com
[^22]: http://developer.mozilla.org/en-US/Add-ons/Extensions/ElasticFox
[^23]: http://www.suchi.com/products/s3fox/
[^24]: http://www.cloudberry.com/cloudberries-explorer/
[^25]: http://www.chambal.com/bucketexplorer/
[^26]: http://www.chambal.com/simpledb-explorer/
[^27]: http://www.ylastic.com/
[^28]: http://www.directthought.com/launch.html#directEC2
