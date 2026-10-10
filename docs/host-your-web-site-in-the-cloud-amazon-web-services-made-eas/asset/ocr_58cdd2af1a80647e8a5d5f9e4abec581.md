# Style

Is the tool a good fit for your working style? Are the command, function, or data structure names consistent and logical? Are your educated guesses correct more often than not? 10

# Security

You'll be trusting these tools with your AWS public and secret keys, so caution is advised. At the very least, you should understand how and where the tool stores your keys and how it protects them from accidental disclosure or casual discovery.

# Language Libraries

Language libraries occupy the space between your application and the web service calls. The libraries provide an adapter that matches the structure and style of the language, so that your application code will look and feel *native*. Some libraries provide an object oriented interface to AWS. All the libraries take care of the details involved in making a call, including handling of default parameter values, managing private and public keys, signing the requests, making the web service calls, checking for error conditions, and parsing returned values into native objects. Some libraries also provide functions to retry calls that have failed due to a transient error; others will accumulate data returned by multiple calls into a single return value.

The official Amazon libraries for PHP are very nice, but as of this writing they lack support for some of the services—S3, for example. If you have no requirement for S3 support, these libraries may fit the bill for you. You can find the EC2 libraries 11 (base EC2, CloudWatch, Auto Scaling, and Elastic Load Balancing), as well as a number of additional libraries for PHP and other languages, at the same link.

In this book we'll be using the CloudFusion library written by Ryan Parman. This library supports all the AWS services. CloudFusion supports multi-threaded access and bulk operations, and is supplied in open source form under the BSD license. 12 CloudFusion also includes a number of high-level utility functions to make AWS even easier to use.

10 I could write an entire book on why I'll never use the word “intuitive” to describe this property, but I have to finish this one first.

11 http://developer.amazonwebservices.com/connect/kbCategory.jspa?categoryId=85

12 http://www.opensource.org/licenses/bsd-license.php