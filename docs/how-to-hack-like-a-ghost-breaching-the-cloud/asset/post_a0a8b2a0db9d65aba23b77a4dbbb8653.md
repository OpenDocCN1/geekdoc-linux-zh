
## 7 BEHIND THE CURTAIN 107
- Kubernetes Overview ................................ 108
- Introducing Pods ................................ 109
- Balancing Traffic ................................ 113
- Opening the App to the World ................................ 115
- Kube Under the Hood ................................ 115
- Resources ................................ 119

## 8 SHAWSHANK REDEMPTION: BREAKING OUT 121
- RBAC in Kube ................................ 122
- Recon 2.0 ................................ 125
- Breaking Into Datastores ................................ 129
- API Exploration ................................ 132
- Abusing the IAM Role Privileges ................................ 135
- Abusing the Service Account Privileges ................................ 136
- Infiltrating the Database ................................ 137
- Redis and Real-Time Bidding ................................ 140
- Deserialization ................................ 141
- Cache Poisoning ................................ 143
- Kube Privilege Escalation ................................ 148
- Resources ................................ 151

## 9 STICKY SHELL 153
- Stable Access ................................ 155
- The Stealthy Backdoor ................................ 160
- Resources ................................ 163

## PART IV: THE ENEMY INSIDE 165

## 10 THE ENEMY INSIDE 167
- The Path to Apotheosis ................................ 168
- Automation Tool Takeover ................................ 172
- Jenkins Almighty ................................ 173
- Hell’s Kitchen ................................ 174
- Taking Over Lambda ................................ 181
- Resources ................................ 185

## 11 NEVERTHELESS, WE PERSISTED 187
- The AWS Sentries ........................................ 188
- Persisting in the Utmost Secrecy ........................................ 190
  - The Program to Execute ........................................ 191
  - Building the Lambda ........................................ 192
  - Setting Up the Trigger Event ........................................ 193
  - Covering Our Tracks ........................................ 195
  - Recovering Access ........................................ 195
- Alternative (Worse) Methods ........................................ 196
- Resources ........................................ 197

## 12 APOTHEOSIS 199
- Persisting the Access: ........................................ 201
  - Understanding Spark ........................................ 204
  - Malicious Spark ........................................ 205
  - Spark Takeover ........................................ 210
  - Finding Raw Data ........................................ 213
- Stealing Processed Data ........................................ 215
  - Privilege Escalation ........................................ 216
  - Infiltrating Redshift ........................................ 220
- Resources ........................................ 224

## 13 FINAL CUT 225
- Hacking Google Workspace ........................................ 226
  - Abusing CloudTrail ........................................ 229
- Creating a Google Workspace Super Admin Account ........................................ 232
- Sneaking a Peek ........................................ 233
- Closing Thoughts ........................................ 235
- Resources ........................................ 235

## INDEX 237

## ACKNOWLEDGMENTS

I would like to express my most sincere thanks to the following:

First and foremost, to Liz Chadwick for her razor-sharp skills and sterling adjustments that helped convey the obscure and sometimes complex messages inside these pages.

To Matt Burrough for diligently and expertly reviewing code, command lines, and anything in between.

To the many people at No Starch Press that worked on this book, from design to copyediting, including Katrina Taylor and Bart Reed. And, of course, to Bill and Barbara for that first meeting that spawned this whole adventure.

To my wife for continuously inspiring me in more ways than one, but most of all for supporting the untimely writing fevers as well as the many frustrated nights it took to put this book together.

To my brother and sister for the conversations that fuel my learning appetite. One such conversation led to my first hacking book eight months later.

Finally, I would like to express my gratitude, love, and admiration for my parents for teaching me to always be curious and aspire for the best.

## INTRODUCTION

![](img/961e81aef23040d0fbe348f58c055860_15_0.png)

The security industry is tricky. I maintain a love/hate relationship with this field, due in no small part to its fickle and fleeting nature. You can spend months or years honing your skills in a particular area of security—say, privilege escalation and lateral movement using PowerShell—only to feel completely useless when you find yourself in a full Linux or macOS environment.

By the time you learn how to dump macOS keychain secrets and defeat Gatekeeper, the new Windows 10 build is out with novel detection measures, rendering every PowerShell attack almost useless. You drag yourself back to the drawing board: blog hunting, conference binging, and researching to upgrade your tools and devise new exploitation pathways. Soberly considered, this rat race may seem like utter madness.

You can, of course, always console your ego by diving into the network of a Fortune 500 company that regards Windows XP/2003 as a precious, endangered species to be preserved at all costs, but the tide is catching up to you. You know in your heart that you have to move on to brighter shores.

At the end of the day, that's what hacking is all about. The frustration of having to throw away a favorite trick can only be matched by the exhilaration of mastering a shiny new technique.

We loosely define *hacking* as an ensemble of tricks and tips designed to achieve unexpected results from a system or a process. Yet, these tricks have an ever-accelerating expiry date. Your aim as a security professional or enthusiast is to seek out and gather as many useful tricks as you can. You never know which spear will stop the bull's charging ahead.

In my other books, I focused a great deal on Windows-related attacks, because most of the Fortune 500 companies designed the majority of their environment around Active Directory. It was the go-to solution to manage thousands of users, servers, and applications.

The zeitgeist is changing, though. A company looking to set up its infrastructure from scratch will no longer spring up a Windows Domain Controller on bare metal in a shared datacenter 20 miles from the city. Really, show me a system admin who still wants to manage hardware obsolescence and an ESXi cluster with 30 appliances with different firewalls, switches, routers, and load balancers. Hand me that noose and close the door already!

Why bother when you can set up everything in a cloud environment in a matter of seconds? Databases, Docker containers, and Active Directory are all but one click away, with a free trial to sweeten the deal for your accountant. Sure, the initial low-ticket fee quickly balloons as your servers scale up, but most startups will be delighted to deal with these types of problems. It means business is growing.

In this book, I have decided to throw away the conventional architecture you find in greasy old companies. Let's see how an attacker might take down a modern and worthy opponent: a company that planted its technical roots in a nurturing and resilient cloud environment, and powered its growth using DevOps practices.

Beyond buzzwords touted by clueless management and hungry headhunters, when followed successfully these new paradigms have such a deep impact on architectural decisions and application designs that they naturally require a new set of tricks and flair to hunt for and find loopholes. Vulnerabilities that may otherwise be overlooked or dismissed in a classic environment suddenly acquire lethal potential in a cloud setting. Forget SQL injection. The second you know that a machine is hosted on Amazon Web Services (AWS), you should focus on another class of vulnerabilities altogether.

Attackers used to hop from one machine to another, sneaking past firewall rules and burrowing their way to the internal database, Active Directory, and what have you. This journey often involved network scans,
