# OffSec

Penetration Testing with Kali Linux

We can use screenshots the steps we take, which will help another tester include them in our report to reproduce the issues. However, we need to be cautious of the audience. A penetration tester may consider an alert window to demonstrate XSS as properly self-explanatory, developers unfamiliar with the vulnerability may not understand its cause or impact. It's good practice to always support a screenshot with text.

Screenshots have a specific goal, which is convey information that would take several sentences to describe or make an impact. In this mind, the screenshot should contain exactly enough information to justify not using text, but shouldn't be too much information to make the screenshot confusing.

To return to the example given in the notes section, we have found XSS in the username field of the application log. We will properly explain the effects of XSS in the actual report. However, the impact of XSS is far easier to show rather than explain without a visual reference as base. We must include evidence of arbitrary JavaScript execution, as well as visual components of the site (i.e. the URL in the browser window). If necessary, secondary or lead-up steps can be captured as well.

A well-constructed screenshot is easy to parse visually. Readers should be able to intuitively understand the picture and its caption without any questions. If there is a greater need for surrounding context, that can be added in a paragraph above or below the image, but the image itself should be understood.

Once again, using an example of XSS in our login form, we will include the following components in the screenshot, resizing the window if necessary. Ideally, we would include the URL as well as some company-specific branding and logos on the form. This lets them know the webpage ties vulnerabilities to their corporate image.

The actual pop-executed in the proof-of-concept is necessary as well, substituted for any more advanced payload as the proof of concept is slowly taken further. Finally, we must ensure that it is all legible. A screenshot that is zoomed in to be properly disrupts the reader's flow. A good screenshot is immediately legible, as shown below.

![](bbox=[0.325, 0.623, 0.674, 0.827])

Figure 11: Good Screenshot

There are several pitfalls we should avoid when using screenshots. We have already discussed making sure the screenshots are legible. We must also ensure there isn't more than one concept