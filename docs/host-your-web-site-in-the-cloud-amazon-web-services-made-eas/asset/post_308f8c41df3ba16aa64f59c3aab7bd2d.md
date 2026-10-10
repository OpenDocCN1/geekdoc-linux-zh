
- Importing Usage Data . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 288
- Querying Account Data . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 294
- Retrieving and Displaying Usage Data . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 296
- Elastic Block Storage . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 302
- EBS from the Command Line . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 302
- EBS Snapshots . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 304
- EBS Public Data Sets . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 308
- EBS RAID . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 309
- EC2 Instance Metadata . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 313
- Dynamic Diagramming . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 317
- Conclusion . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 329

- **Chapter 11: Putting It All Together: CloudList**
- Designing the Application . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 331
- Utility Functions and Programs . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 332
- The Web Front End . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 344
- The New Item Submission Form . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 349
- And That's It . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 354

- Index . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 355

## Preface

In the spring of 2002, I logged in to my Amazon Associates account one day and saw a little box on the landing page with the magic words: “Amazon Now Has XML!” Amazon had exposed many aspects of its product catalog in XML form. Coupled with the Amazon Associates program, enterprising developers could download the data, use it to create a marketing site, and then earn commissions by sending traffic to the main Amazon.com site.

I thought this was fairly interesting and dived right in. I downloaded the documentation, wrote some code, and was impressed. I saw plenty of promise, but also plenty of room for improvement, so I wrote it all up and sent it to a feedback email address that they’d provided for this purpose.

One situation led to another and by early summer I was Amazon’s guest at a very exclusive conference held at their headquarters. They had invited five or six outside developers to Seattle in order to gain some direct customer feedback on their service and talk about their plans for the future. As I sat there and listened, I was definitely impressed. It was clear they were thinking big. They hinted at their plans to open up the Amazon technology platform and invite developers to participate.

Having worked at Microsoft for three years, I had a real appreciation for a platform’s power and my mind raced forward. They were going to need a developer program, sample code, more documentation, and all sorts of material in order to make this happen. I thought I could make a contribution, and stepped out to chat with the person who’d extended the invitation to me; I told her I wanted to interview for a role at Amazon to work on this new web services effort!

In order to demonstrate my interest in Amazon, I wrote a set of PHP wrappers for that very first version of AWS and called it PIA, the PHP Interface to Amazon. Amusingly enough, my now quaint announcement can still be found on the AWS Discussion Forums.<sup>1</sup>

I went through the interview process, and before the end of the summer I was hired as a senior member of the Amazon Associates team. My official duty was to write business analytical tools using Perl; however, my manager also indicated that I should devote 10–20% of my time to helping out on the web services effort in whatever way seemed appropriate.

Just a few weeks after I started, the manager of the Amazon Associates team asked me if I would mind speaking at a conference. She explained that they had intended to hire a “real” speaker when she accepted the invitation, but it was taking longer than expected to find the right person. I did a lot of public speaking earlier in my career and was happy to take care of this for them. That first event went really well, and before too long they tossed another one my way, and then another. The 10–20% of time allocated to the web services effort quickly grew to 40–50%; I kept busy writing sample code, answering questions on the AWS forums, and doing whatever I could to help the first members of our developer community succeed.

A few months passed and management approached me. “We’ve been planning to hire an evangelist to take on these speaking gigs, but it appears that you’re already doing most of the job. Do you want it?” After some consultation with my family, I decided that I did, and in April of 2003 it was made official. I was the world’s first (as far as I know) Web Services Evangelist!

In this role I travel the world and speak at a range of forums: conferences, user groups, college classes, and corporate technology teams. I arrange one-on-one meetings with developers in each city, and use these meetings to learn about what the developers are doing and how we can better serve them.

Over the last couple of years we’ve released a number of infrastructure services, including the Elastic Compute Cloud (EC2), the Simple Storage Service (S3), the Simple Queue Service (SQS), and the Simple Database (SimpleDB). It has been a real privilege to watch firsthand as the AWS team has designed, implemented, delivered, and operated service after service to see our developer community grow to include hundreds of thousands of developers.

When I was asked to consider writing a book about AWS earlier this year, I thought it would be the perfect opportunity to share some of what I’ve learned in the last seven years.

## Thanks for Reading

I hope that you enjoy reading this book as much as I’ve enjoyed writing it. Please feel free to look me up and let me know what you think.

## Who Should Read This Book?

This book is aimed at web developers who have built a web application or two, and are ready to leap into the world of cloud computing using Amazon Web Services. This book makes use of the PHP language, but if you have experience in any server-side scripting language, you’ll find the examples clear and easy to understand. It’s also assumed that you know the fundamentals of HTML and CSS, and that you’re comfortable with the Linux command line. Knowledge of basic system administration tasks, such as creating and mounting file systems, will also be helpful.

By the end of this book, you can expect to have a firm grasp of the concept of cloud computing and its role in enabling a whole new class of scalable and reliable web applications. You’ll also have gained a clear understanding of the range of Amazon Web Services, such as the Simple Storage Service, the Elastic Compute Cloud, the Simple Queue Service, and SimpleDB. You’ll be able to make use of all these services in your web applications as you write commands, tools, and processes in PHP.

## What’s Covered in This Book?

The book comprises 11 chapters. Chapters 3 through to 10 detail specific Amazon Web Services, and the final chapter explores building a sample application. I would recommend that you read the book from start to finish on your first go, but keep it by your side to dip in and out of the chapters if you need a refresher on a particular web service.

**Chapter 1: Welcome to Cloud Computing**

In this chapter, you’ll learn the basics of cloud computing, and how it both builds on but differs from earlier hosting technologies. You will also see how organizations and individuals are putting it to use.

**Chapter 2: Amazon Web Services Overview**

This chapter moves from concept to reality, where you’ll learn more about the fundamentals of each of the Amazon Web Services. Each web service is explained in detail and key terminology is introduced.

**Chapter 3: Tooling Up**

By now you’re probably anxious to start. But before you jump in and start programming, you’ll need to make sure your tools are in order. In Chapter 3, you’ll
