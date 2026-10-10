
## Prerequisites and Setup

the downloaded file archive and move the resulting **cloudfusion** directory to the location where you’d like CloudFusion to be installed.

-   Modify the PHP `include_path` setting in your `php.ini` file; this is to include the full path to the location of the CloudFusion library files.
    -   On a Linux system, this file is found in the `/etc` directory (as well as on Mac OS X). I put CloudFusion in the `/mnt/cloudfusion` directory, so I edited the `include_path` to look like this:

        ```
        include_path = ":./php/includes:/mnt/cloudfusion"
        ```

    -   If you’re on a Windows machine your `php.ini` file will be found in your PHP installation folder. If you’ve placed the CloudFusion files in `c:\cloudfusion`, this is what your `include_path` statement will look like:

        ```
        include_path = ":;c:\php\includes;c:\cloudfusion"
        ```

    -   You should also create a folder for the source code for all the examples in this book; then, download the code and append that directory name to the `include_path` as well.

-   Now turn your attention to the CloudFusion directory. Copy the file **config-sample.inc.php**, rename it **config.inc.php**, and open this new file for editing. Locate the following statements:

    ```
    define( 'AWS_KEY', '');
    define('AWS_SECRET_KEY', '');
    ```

    -   Edit the first statement so that your access key ID is between the quotes. Edit the second statement so that your secret access key is between quotes, like so:

        ```
        define( 'AWS_KEY', 'your_access_key_id');
        define( 'AWS_SECRET_KEY', 'your_secret_access_key');
        ```

    -   If other people can access the computer where you’ve stored your keys, take appropriate steps to protect both the computer and this file from disclosure.

-   Delete your scratch file.

## Where We've Been

In this chapter we talked about the technical prerequisites that you'll need in order to gain the most possible value from the rest of the book. We started tooling up, re- viewing a few of the many programming libraries, command line tools, and visual tools available for AWS. We stepped through the AWS registration process and obtained an account with a key to access the web services. We also installed the Cloudfusion library. We're now ready to begin coding.

# Chapter 4

## Storing Data with Amazon S3

In this chapter, we'll dive headfirst into Amazon S3, the Simple Storage Service. After a quick overview of the most important S3 concepts, we'll spend the greater part of this chapter reviewing the code needed to manipulate buckets and objects in S3 and its content-distribution sibling, CloudFront.

### S3 Overview

S3 is an Internet-scale data storage service. All data is stored redundantly to guard against problems brought on by temporary connectivity issues or permanent hard-ware failures. S3 can scale to handle vast amounts of data and deal with a very large number of concurrent accesses. At the time of writing, S3 held over 124 billion objects and was handling over one trillion requests per year.[^1]

S3 lets you store your data in containers called **buckets**. A bucket is a named storage entity attached to a particular AWS account. You can create up to 100 buckets in your AWS account. The bucket names must be globally unique, so you'll have to choose with care and keep on trying until you find available names.

[^1]: http://aws.amazon.com/about-aws/whats-new/2009/03/30/celebrating-3-years-of-amazon-s3-with-3-months-of-transfer-in-for-3-centsb/

Buckets are used to group any number of S3 objects. When I say any number, I really mean it—it is perfectly reasonable to store millions or tens of millions of objects in a single S3 bucket. Depending on your needs, you may choose to use a number of buckets for a single application, or you may choose to use a single bucket for each application.

You can store any type of data you like in S3. It could be text files such as HTML pages, CSS style sheets, or C source code, or binary files such as JPEG images, tar backup files, or even encrypted data (you can encrypt sensitive data before storing it in S3, if you’d like). S3 is ideal for storing web data. Each S3 object has its own URL and S3 can handle a very high request rate.

S3 can store objects of up to 5GB in size. This is a limit that you’ll probably never approach in practice, due to various factors. Depending on the speed of your internet connection, it could take hours or even days to upload an object of this size. If the connection was interrupted, you’d have to restart the upload from the beginning. Also, some of the S3 tool kits attempt to read the entire object into memory before uploading it.

Every S3 object has a unique URL formed by concatenating these components:

-   protocol (`http://` or `https://`)
-   bucket name ending with `.`
-   S3 endpoint (`s3.amazonaws.com`)
-   object key starting with `/`

The object key can itself contain `/` characters. These characters are simply part of the object’s name and have no special meaning to S3. S3 is not a hierarchical file system and has no concept of a subfolder. The S3 tools listed in Chapter 3 maintain the polite fiction that the `/` is special and allows the user to traverse the contents of an S3 bucket as if it contained actual subfolders.

S3 can be accessed using either one of two APIs. The SOAP API contains functions such as ListAllMyBuckets, CreateBucket, and DeleteBucket. The HTTP API uses the standard HTTP verbs (GET, PUT, HEAD, and DELETE) as the basis for all operations. The GET operation retrieves the contents of a bucket or an object, the PUT operation creates a new bucket or object, the DELETE operation removes a bucket or an object, and the HEAD operation retrieves information about an object.

You can attach metadata in the form of key-value pairs when you create a new S3 object. The metadata is returned in the form of HTTP headers when the object is retrieved using an HTTP GET request.

Access to each S3 bucket and object is regulated by an **ACL** or **Access Control List**. An ACL contains a series of up to 100 **grants**, with each grant consisting of a **grantee** and a **permission**. Using the ACL, you can grant access to specific users or to groups of users.

Specific users represent an individual AWS account. The account can be specified using an email address or a canonic user ID, but it is always returned as a `CanonicalUser` object—the email address is simply a convenience.

Groups represent predefined classes of users, any AWS user, or anonymous users (anyone at all).

The permission component of a grant in an ACL specifies the access given to the related grantee. You can grant permissions to buckets or to objects—but be aware that the semantics are slightly different for each, as described in Table 4.1.

**Table 4.1. S3 Permission Grants When Applied to Buckets and Objects**

| Permission | When applied to a bucket | When applied to an object |
|:-----------|:-------------------------|:-------------------------|
| `READ` | Permission to list the contents of the bucket | Permission to read the object or its metadata |
| `WRITE` | Permission to create, replace, or delete any object in the bucket | Unsupported for objects |
| `READ_ACP` | Permission to read the bucket's ACL | Permission to read the object's ACL |
| `WRITE_ACP` | Permission to overwrite the bucket's ACL | Permission to overwrite the object's ACL |
| `FULL_CONTROL` | All of the above | All of the above |

The owner of a bucket or an object always has implicit `READ_ACP` permission; you can always access the ACL of your own objects. Similarly, the owner also has implicit `WRITE_ACP` permission, so you can always change the ACL of your own object too. The `FULL_CONTROL` permission is provided for convenience and has the same effect as applying the READ, WRITE, `READ_ACP`, and `WRITE_ACP` permissions.

Permissions on buckets and objects are distinct. The bucket's permissions have no influence on the permissions of newly uploaded objects; ACLs must be set separately for each new object.

## The S3 Pricing Model

Your S3 usage is charged in three dimensions:

-   amount of data stored
-   amount of data transferred in and out of S3
-   the number of requests made to S3

Let’s examine each of these dimensions in detail.

Your S3 storage charges are based on a unit known as a **gigabyte-month**. If you store exactly one gigabyte for exactly one month, you’ll be charged for one gigabyte-month, which is $0.15 (fifteen cents).[^2] Time and space can be traded for one another, so you could also store two gigabytes for half of a month for $0.15, or even 30 gigabytes for one day if you’d like. Internally, S3 uses a more fine-grained billing unit, a **byte-hour**. This allows AWS to measure your usage with a very high degree of accuracy and to bill you accordingly.

Your data transfer charges are based on the amount of data transferred in (uploaded) and out (downloaded) from S3. Data transferred in to S3 is charged at a rate of $0.10 per gigabyte. Once again, this amount is prorated. Data transferred out of S3 is charged on a sliding scale starting at $0.17 per gigabyte and decreasing based on volume, reaching $0.10 per gigabyte for all outgoing data transfer in excess of 150 terabytes per month. As an important special case, there is no charge to transfer data between S3 and an Amazon EC2 instance in the same Region.

There are also nominal (yet important) charges for each request made to S3. HTTP **GET** requests are charged at the rate of $0.01 for every 10,000 requests. **PUT**, **COPY**, **LIST**, and **POST** requests are charged at the rate of $0.01 for every 1,000 requests.

Putting it all together, this pricing model means that you can probably prototype and then run your S3-powered application for next to nothing, paying for more storage and more data transfer only as your application becomes popular.

[^2]: Footnote marker corrected from OCR artifact.
