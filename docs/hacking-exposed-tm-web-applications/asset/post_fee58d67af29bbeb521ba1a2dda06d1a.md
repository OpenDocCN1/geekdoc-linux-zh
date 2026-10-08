
## Preface: XXV

We have also followed the Hacking Exposed line when it comes to countermeasures, which follow each attack or series of related attacks. The countermeasure icon remains the same:

# This Is a Countermeasure Icon

This should be a flag to draw your attention to critical fix information.

# Other Visual Aids

We've also made prolific use of visually enhanced

![](img/2c61c2d28445b774d9266972920f432d_25_0.png)

![](img/2c61c2d28445b774d9266972920f432d_25_1.png)

![](img/2c61c2d28445b774d9266972920f432d_25_2.png)

icons to highlight those nagging little details that often get overlooked.

## ONLINE RESOURCES AND TOOLS

Web app security is a rapidly changing discipline, and we recognize that the printed word is often not the most adequate medium to keep current with all of the new happenings in this vibrant area of research.

Thus, we have implemented a World Wide Web site that tracks new information relevant to topics discussed in this book, errata, and a compilation of the public-domain tools, scripts, and dictionaries we have covered throughout the book. That site address is:

```
http://www.webhackingexposed.com
```

It also provides a forum to talk directly with the authors via e-mail:

joel@webhackingexposed.com
mike@webhackingexposed.com

We hope that you return to the site frequently as you read through these chapters to view any updated materials, gain easy access to the tools that we mentioned, and otherwise keep up with the ever-changing face of Web security. Otherwise, you never know what new developments might jeopardize your applications before you can defend yourself against them.

## A FINAL WORD TO OUR READERS

There are a lot of late nights and worn-out mouse pads that went into this book, and we sincerely hope that all of our research and writing translates to tremendous time savings for those of you responsible for securing Web applications. We think you've made a courageous and forward-thinking decision to stake your claim on a piece of the Internet—but as you will find in these pages, your work only begins the moment the site goes live. Don't panic—start turning the pages and take great solace that when the next big security calamity hits the front page, you won't even bat an eye.

> —Joel & Mike

## PART I

## RECONNAISSANCE

## CHAPTER 1

![](img/2c61c2d28445b774d9266972920f432d_29_0.png)

## 4 Hacking Exposed Web Applications

Remember the early days of the online revolution? Command-line terminals, 300 baud modems, BBS, FTP. Later came Gopher, Archie, and this new, new thing we called Netscape that could render online content in living color, and we began to talk of this thing we called the World Web...

How far have we come since the early 90s! Despite those few remaining naysayers who still use the words "dot com" with dripping disdain, the Internet and, in particular, the World Wide Web have radiated into every aspect of human activity like no other phenomenon recorded in history. Today, over this global communications medium, we can just almost instantaneously

- Purchase a nearly unlimited array of goods and services, including housing, cars, airline tickets, computer equipment, and books, just to name a few
- Perform complex financial transactions, including banking, trading of securities, and much more
- Find well-researched information on practically every subject known to humankind
- Search vast stores of information, readily pinpointing the one item you require from amongst a vast sea of data
- Experience a seemingly limitless array of digital media content, including movies, music, images, and television
- Access a global library of incredibly diverse (and largely free) software tools, from operating systems to word processors
- Communicate in real time with anyone, anywhere, for little or no cost using Web-based e-mail, telephone, or chat

And this is just the beginning. The Web is evolving as we speak into something more than its incarnation, becoming easier to use, more accessible, full of even more data, and more functional with each passing moment. Who knows what tomorrow holds in store for this great medium?

Yet, despite this immense cornucopia enjoyed by millions every day, very few understand how it works, even at the most basic technical level. Few still are aware of the inherent vulnerability of the technologies that underlie the applications running on the World Wide Web and the ease with which many of them fall prey to online vandals or even more insidious foes. Indeed, it is a fragile Web we have woven.

We will attempt to show you exactly how fragile throughout this book. Like the other members of the Hacking Exposed series, we will illustrate this fragility graphically with examples from our recent experiences working as security consultants for large organizations where we have identified, exploited, and recommended countermeasures for issues exactly as presented in these pages.

## Chapter 1: Introduction to Web Applications and Security

Our goal in this first chapter is to present an overview of Web applications, where common security holes lie, and our methodology for uncovering them before someone does. This methodology will serve as the guiding structure for the rest of the book—each chapter is dedicated to a portion of the methodology we will outline here, covering each step in detail for technical readers to implement countermeasures, while remaining straightforward enough to make the material accessible to lay readers who don't have the patience for a lot of jargon.

Let's begin our journey with a clarification of what a Web application is, and where it lies in the overall structure of the Internet.

## THE WEB APPLICATION ARCHITECTURE

Web architectures most closely approximate the centralized model of computing, with many distributed “clients” that typically perform little more than data presentation to a central “thick” server that does the bulk of the processing. What sets Web architectures apart from traditional centralized computing models (such as mainframe computing) is that they rely substantially on the technology popularized by the World Wide Web, the Hypertext Markup Language (HTML), and its primary transport medium, Hypertext Transfer Protocol (HTTP).

Although HTML and HTTP define a typical Web application architecture, there is a lot more to a Web app than these two technologies. We have outlined the basic components of a typical Web app in Figure 1-1.

In the upcoming section, we will discuss each of the components of Figure 1-1 in turn (don't worry if you're not immediately familiar with each and every component of Figure 1-1; we'll define them in the coming sections).

![](img/2c61c2d28445b774d9266972920f432d_31_0.png)

## Hacking Exposed Web Applications

## A Brief Word about HTML

Although HTML is becoming a much less critical component of Web applications as we write this, it wouldn't just be appropriate to omit it completely since it was so critical to the early evolution of the Web. We'll give a brief overview of the language here, since there are several voluminous primers available that cover every aspect (the complete HTML specification can be found at the link listed in the "References and Further Reading" section of this chapter. Our focus will be on the security implications of HTML.

As a markup language, HTML is defined by so-called tags that define the format or capabilities of document elements. Tags in HTML are delimited by angle brackets < and >, define a broad array of formats and functionalities as defined in the HTML specification. Here is a simple example of basic HTML document structure.

```
<HTML>
<h1>This is a First-Level Header</h1>
<p>This is the first paragraph.</p>
</HTML>
```

When displayed in a Web browser, the tags are interpreted and the document elements are defined by the format or functionality defined by the tags, as shown in the next illustration (we'll discuss Web browsers shortly).

![](img/2c61c2d28445b774d9266972920f432d_32_0.png)

As we can see in this example, the text enclosed by the <h1>...</h1> brackets are formatted with a large, boldfaced font, while the <p>...</p> text takes on a format appropriate for the body of the document. Thus, HTML primarily serves as the data presentation engine of a Web application (both server- and client-side).

As we've noted, a complete discussion of the numerous tags supported in the current HTML spec would be inappropriate here, but we will note that there are a few tags that could be used to deleterous effect by malicious hackers. Most commonly used tags are related to taking user input (which is done using the <INPUT> tag, you wouldn't know).
