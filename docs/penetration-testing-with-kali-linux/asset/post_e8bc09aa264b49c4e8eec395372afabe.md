
# OffSec

Penetration Testing with Kali Linux

We can use screenshots the steps we take, which will help another tester include them in our report to reproduce the issues. However, we need to be cautious of the audience. A penetration tester may consider an alert window to demonstrate XSS as properly self-explanatory, developers unfamiliar with the vulnerability may not understand its cause or impact. It's good practice to always support a screenshot with text.

Screenshots have a specific goal, which is convey information that would take several sentences to describe or make an impact. In this mind, the screenshot should contain exactly enough information to justify not using text, but shouldn't be too much information to make the screenshot confusing.

To return to the example given in the notes section, we have found XSS in the username field of the application log. We will properly explain the effects of XSS in the actual report. However, the impact of XSS is far easier to show rather than explain without a visual reference as base. We must include evidence of arbitrary JavaScript execution, as well as visual components of the site (i.e. the URL in the browser window). If necessary, secondary or lead-up steps can be captured as well.

A well-constructed screenshot is easy to parse visually. Readers should be able to intuitively understand the picture and its caption without any questions. If there is a greater need for surrounding context, that can be added in a paragraph above or below the image, but the image itself should be understood.

Once again, using an example of XSS in our login form, we will include the following components in the screenshot, resizing the window if necessary. Ideally, we would include the URL as well as some company-specific branding and logos on the form. This lets them know the webpage ties vulnerabilities to their corporate image.

The actual pop-executed in the proof-of-concept is necessary as well, substituted for any more advanced payload as the proof of concept is slowly taken further. Finally, we must ensure that it is all legible. A screenshot that is zoomed in to be properly disrupts the reader's flow. A good screenshot is immediately legible, as shown below.

![](img/336d6ea891e7464f18ad64426619ced4_97_0.png)

Figure 11: Good Screenshot

There are several pitfalls we should avoid when using screenshots. We have already discussed making sure the screenshots are legible. We must also ensure there isn't more than one concept illustrated in each screenshot. A screenshot that contains two pieces of pertinent information does not itself to be easily understood at a glance. We must ensure it is framed properly in the screenshot. Having the target of the screenshot off-center in the site obfuscates the intent. Well, the caption for the screenshot shouldn't be overly long.

![](img/336d6ea891e7464f18ad64426619ced4_98_0.png)

Figure 12: Bad Screenshot

The screenshot covers the important information with an irrelevant piece of information, which prevents the full impact of the screenshot from being understood by the reader.

To recap, a good screenshot has the following characteristics:

- is legible
- contains some visual indication that it applies to the client
- contains the material that is being described
- supports the description of the material
- properly frames the material being described

On the other hand, a bad screenshot is one that:

- is legible
- is generic rather than client-specific
- contains obfuscated or irrelevant information
- is improperly framed

Under the screenshot, we include a caption. A caption is not meant to provide additional context for the picture. A caption is to describe the picture in a few words. Any additional context that is necessary can be provided in a separate paragraph. In most cases, eight to ten words is an appropriate maximum for a caption.

## 5.1.6 Tools to Take Screenshots

We can take screenshots using operating system capabilities. Windows, Linux, and macOS all provide tools to take screenshots. We can also use special-purpose tools.

For Windows, the PrintScreen allows us to take a copy of the full screen, and Alt/PrSc takes a screenshot of your currently active window. This can then be pasted into a Paint, Word, or Powerpoint document and manipulated as required. We'll often want to crop the image to remove any unwanted material, and we can do that in these applications.

We can also invoke the Windows Snipping Tool^205 by pressing the Windows key with Shift/S.

![](img/336d6ea891e7464f18ad64426619ced4_99_0.png)

Figure 13: Snipping Tool

The Snip tool allows us to highlight and take a snapshot of any area of the screen we choose.

MacOS provides the capability to take a screenshot using the keyboard Shift/Command combination with the numeric keys 3, 4, or 5. To select and save the entire screen, we can use Shift+3 or Shift+4 to highlight and select a specific area on the screen, we can simply use Shift+5 or Shift+6.

We can take a screenshot in Linux using the PrintScreen. This will capture and save the entire screen to the user's **images/** directory. Shift+PrintScreen will allow for highlighting and selection. In Kali Linux, we can also use the Snippet tool which is installed by default and comes with many options such as choosing the active window, selecting a region, adding a delay before taking the actual screenshot, etc. Flameshot^206 is an OS-agnostic, open-source, feature-rich screen-capturing tool. It comes with command line and GUI interface that add highlights, pixelation, and other modifications to the captured image. ^205 (Wikipedia, 2022). https://en.wikipedia.org/wiki/Snipping_Tool ^206 (Flameshot, 2022). https://github.com/flameshot-org/flameshot

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

## 5.2 Writing Effective Penetration Testing Reports

In this Unit we will cover the following Learning Objectives:

- Identify the purpose of a report
- Understand how to specifically tailor content
- Construct an Executive Summary
- Account for test environment considerations
- Create technical summary
- Describe technical findings and recommendations
- Recognize when to use appendices and references

### 5.2.1 Purpose of a Technical Report

As vendors of a service, we want to provide our clients with as much value as possible. Reports are the mechanism by which value is delivered and the main artifact that enables the client to take action. Our ability to find vulnerabilities won't make a business impact if we can't provide a presentation of both the vulnerabilities and recommendations. Without a clear direction forward, the client is not getting value for their time and money.

To properly prepare a report for the client, we must understand two things:

1. The purpose of the report.
2. How we can deliver the information we've collected in a way that the audience can understand.

When a client pays for a penetration testing engagement, it is often (mis)understood that they are “just” paying for an ethical hacker to legally attack their infrastructure and exploit weaknesses. While it may be technically necessary to deliver the required results, it is not the fundamental purpose of the engagement. So, what is the goal of a company engaging a penetration test? The goal is for the client to be presented with a path that outlines and highlights the flaws that are currently present in their systems within the scope of the engagement, ways to fix those flaws in an immediate sense, and strategic goals that will prevent vulnerabilities from appearing in the future. This is often provided in the form of a penetration testing report. As far as the client is concerned, the report is (usually) the only deliverable of the engagement that truly matters.

We might wonder how to report the parts of an engagement where we haven't found vulnerabilities. In many cases where we don't find vulnerabilities, we should avoid including too many technical details on what we did in the report. A simple statement that no vulnerabilities were found is often enough. We should ensure that we don't confuse the client with the details of our attempts, as this will undermine the value of the issues we did find it's the tester's job to present that information in a way that is easy to understand and act upon.
