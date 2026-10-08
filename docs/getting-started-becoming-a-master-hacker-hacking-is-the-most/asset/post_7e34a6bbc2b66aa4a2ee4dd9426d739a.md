
Congratulations! You are now ready to embark on a journey of “a thousand steps!” Be patient with yourself, you will not become a Master Hacker overnight, but you have taken the first important steps in that journey.

# 5

## Passive Reconnaissance

***“ Listen” closely and intently to your enemy; they will tell you everything you need to know to defeat them*** **Master OTW**

**Many on this path to becoming a master hacker** tend to discount the need to do information gathering or reconnaissance. These newbies (I don't use that as a term of disparagement, but as a descriptor. We all began as newbies) want to rush right into attacking a target system. The master hacker understands that the more they know about the target, the better their chances of success. As I mentioned earlier in Chapter 3 on the “Hacker Process,” reconnaissance may take up to 90 percent of the entire project time and, in some cases, may take months.

This chapter will focus on gathering information about our target from publicly available sources. These techniques are often termed "passive reconnaissance" because the hacker gathers information without interacting with the target. Some people also refer to this as open-source intelligence (OSINT). All of the information comes from third-party sources who have already gathered the information about our target.

The information you gather in this stage depends upon the target. If the target is a website, you want to know as much about the technologies behind the web site as possible. If the target is a domain, you want to know as much about the domain as possible. If the target is a person, you want to know as much as possible about the person.

It would be impossible to include all the passive-reconnaissance techniques, so we will limit ourselves to just a few here:
- 1. Google Hacking
- 2. Netcraft
- 3. Shodan
- 4. DNS
- 5. p0F

For additional passive reconnaissance techniques, go to www.hackers-arise.com/osint.

### Hacking Google

As we all know, Google operates the most widely used Internet search engine on the planet. Google crawls nearly every web page of every web site, and builds a massive database of all the information it gathers. Most people then use Google's database to search by **keywords** for articles relevant to the subject of their inquiry. Google then retrieves the most relevant web sites based upon its algorithm (the PageRank algorithm, named for Larry Page, one of Google’s founders), which prioritizes the articles.

What few know is that Google has particular keywords and operators that can assist you in extracting precise information from this extraordinary database. As a hacker, that Google database may yield information about potential targets that could prove invaluable, including passwords.

Let's take a look at a few of those keywords and what they do.

**Google Hacking Keywords** Please note that **Google's keywords require a colon(:) between the keyword and the search terms**, such as *intitle:hackers-arise*.

Although far from an exhaustive list, here are some of the more widely used Google keywords:

**allinanchor**
If you use the allinanchor keyword, Google restricts your search to those web pages that have ALL of the terms you are looking for in the anchor of the page.

**allintext**
If you use the allintext keyword, Google restricts your search to those pages that have ALL of the search terms you specify in the text of the page.

**allintitle**
If you use the allintitle keyword, Google restricts your search to those pages that have ALL of the search terms you specify in the title of the page.

**allinurl**
If you use the allinurl keyword, Google restricts your search to those pages that have ALL of the search terms you specify in the URL of the page.

**filetype**
If you use the filetype keyword, Google restricts your search to those pages that have the filetype you specify. For instance, to search for an Adobe PDF file, you could use `filetype:pdf`.

**inanchor**
If you use the inanchor keyword, Google restricts your search to those pages that have search terms you specify in the anchor of the page.

**intext**
If you use the intext keyword, Google restricts your search to those pages that have the search terms you specify in the text of the page.

**intitle**
If you use the intitle keyword, Google restricts your search to those pages that have the search terms you specify in the title of the page.

**inurl**
If you use the inurl keyword, Google restricts your search to those pages that have the search terms you specify in the URL of the page.

**link**
When you use the link keyword followed by the URL, Google shows you all the sites that link back to the specified URL.

**site**
If you use the site keyword, Google restricts your search to the site or domain you specify.

### Google Hacking Examples

Let’s look at some examples of how we can use Google hacking to find relevant web sites and files.

As you know, many firms store important financial and other information in Excel files. We could use a simple Google hack that looks for the Excel filetype, “.xls” or “.xlsx”.

```
filetype:xls
```

We can get a bit more selective and combine Google keywords to look for Excel files in government websites (by using the keyword **site** with the top level domain **.gov** ) that have the word "contact" in their URL. This yields web pages that have contact lists from government agencies, a possible treasure trove for social engineering (see Chapter 17 for “Social Engineering”).

```
filetype:xls site:.gov inurl:contact
```

**Search Results Example:**

- Web
- Images
- Videos
- Maps
- Books
- More
- Search tools

About 377 results (0.27 seconds)

1. **[XL9] HRD Contact - Mass.Gov**
   www.mass.gov/anf/docs/hrld/modules/hrld-contact.xls
   > Massachusetts > A, B, C, 1, Telephone: 2, 3, (617) 727-3555 (HRD Main Office), 4, 1-800-392-6178 (Toll Free Number), 5, (617) 878-9762 (TTY), 6, 7, Fax Number: View unit Fax ...

2. **[XL9] 2015 Agency Contact Directory - Oregon.gov**
   www.oregon.gov/...2015%20Agency%20Contact%20Directory...
   > Oregon > A, B, C, D, E, F, G, 1, Agency, Name, E-mail Address, Title, Phone, Address, City/ State/Zip, 2, Accountancy, State Board of, Prittoni, Martin ...

3. **[XL8] District Preschool Contact.xls**
   education.ky.gov/educational/pre/.../District%20Preschool%20Contact...
   > A, B, C, D, E, F, G, H, I, J, K, 1, DISTRICT, RTC, Preschool Coordinator Name, Street Address, City, Zip Code, Email Address, Phone Number, Fax.

4. **[XL5] H1N1 Supplemental Contact Follow-up Form - State of ...**
   www.cdph.ca.gov/.../Supplement...
   > California Department of Public Health > A, B, C, D, E, F, G, H, I, J, K, L, M, N, O, 1, Total number of household, intimate and daycare/childcare contacts since the case's first day of symptom onset ...

5. **[XL5] National School Lunch Program Public Contact List**
   www.doe.in.gov/sites/default/files/.../nslp-public-contact-list.xls
   > Indiana > A, B, C, D, E, F, G, H, I, J, K, L, M, N, O, P, 1, TYPE, CONO, CONA, CDPB, NAME, PUBPRIV, SALU, FIRSTNME, LASTNME, TITLE, ADDRESSEE, ADDR1 ...

6. **[XL5] CACFP Public Contact List - Indiana Department of Educ...**
   www.doe.in.gov/sites/default/files/.../cacfp-public-contact-list.xls
   > Indiana > A, B, C, D, E, F, G, H, I, J, K, L, M, N, O, P, 1, TYPE, CONO, CONA, SPONSORBR, SPONSORNME, PUBPRIV, SALU, FIRSTNME, LASTNME, TITLE ...

7. **[XL5] Contact List.xls**
   ftp://ftp.cdc.gov/.../...
   > United States Centers for Disease Control and Prevention > A, B, C, D, E, F, G, H, I, J, K, L, 1, Report of Verified Case of Tuberculosis Training Contact List of Participants, Observers, and Facility <Insert Date>, 2, Course ...
