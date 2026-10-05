two fibers but both are in the same conduit, or it may be that the backup connec-
tion transits an already saturated ATM cloud. Hold a yearly review with your ISPs
to verify that you still have genuine redundancy.

# Security incidents

System security is covered in detail in Chapter 22, Security. However, it's worth
mentioning here because security considerations impact the vast majority
of administrative tasks. There is no aspect of your site's management strategy that
can be designed without regard for security. For the most part, Chapter 22
concentrates on ways of preventing security incidents from occurring. However,
thinking about how you might recover from a security-related incident is an
equally important part of security planning.

Having your site hijacked is a particularly embarrassing type of break-in. For
the sysadmin at a web hosting company, a hijacking can be a calamitous event,
espec when it involves sites that handle credit card data. Phone calls stream in
from customers, from the media, from the company VIPs who just saw the news
of the hijacking on CNN. Who will take the calls? What should they say?
Who is in charge? What role does each person play? If you are in a high-visibility
business, it's definitely worth thinking through this type of scenario, coming up
with planned answers, and perhaps even having a practice session
to work out the details.

Sites that accept credit card data have legal requirements to deal with a hi-
jacking. Make sure your organization's legal department is involved in security
incident planning, and make sure you have relevant contact names and phone
numbers to call in a time of crisis.

When CNN or Slashdot announces that your site is down, the same effect
makes highway traffic down to look at an accident on the side of the
road causes your Internet traffic to increase enormously, often to the point of
breaking whatever that you just fixed. If your site cannot handle an
increase in traffic of 25% or more, consider having your load balancing device
route excess connections to a server that presents a page that says "Sorry,
we are too busy to handle your request right now."

Develop a complete incident handling guide to guide the guesswork of manag-
incident security problems. See page 950 for more details on incident management.

# 32.9 COMPLIANCE: REGULATIONS AND STANDARDS

IT auditing and governance are big issues today. Regulations and quasi-standards
for specifying, measuring, and certifying compliance have spawned myriad ac-
nyms: SOX, ITIL, COBIT, and ISO 27002, just to name a few. Unfortunately, this
alphabet soup is leaving something of a bad taste in system administrators'
mouths, and software to implement all the controls deemed necessary by recent
legislation is currently lacking.