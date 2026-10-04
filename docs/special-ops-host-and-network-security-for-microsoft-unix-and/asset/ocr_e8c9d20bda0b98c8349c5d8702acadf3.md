# Chapter 11 • Hacking Custom Web Applications

+   * Automatic Web application vulnerability tools such as SPIKEProxy
WhiteHat Arsenal are getting smarter all the time.

+   * Hack your site, before someone else does!

# Frequently Asked Questions

The following Frequently Asked Questions, answered by the authors of this book, are designed to measure your understanding of the concepts presented in this chapter and to assist you with real-life implementation of these concepts. To have your questions about this chapter answered by the author, browse to www.syngress.com/solutions and click on the ‘Ask the Author’ form.

**Q**: What is the difference between a Web server and a Web application? Can a Web server vulnerability affect a Web application?

**A**: Web servers are typically tightly coupled with the operating system they run on, and are normally bought off the shelf (or downloaded from the Web). They typically have an enormous install base and are widely supported. Web applications, however, run within or on top of these Web servers and are custom written. Although a Web server vulnerability need not imply a vulnerability within the Web application running on top of it, the tightly coupled nature of these two often mean that a vulnerability in one aids an attacker in gaining control of the other.

**Q**: I plan on deploying a Web application to handle customer information. My choice of platform important from a security point of view?

**A**: Although operating system wars are normally based on personal bias than actual merit, be in mind that there are indeed differences between the different platforms and their default security stances. A wise option would be to base the decision on the platform on the exact requirements for the specified application.

**Q**: Doesn’t the use of SSL on my site mean that it is secure?

**A**: A common misconception is that SSL “secures” your Web site. SSL enables a degree of privacy by facilitating encryption on the wire (SSLv3 allows for authentication). SSL only protects the confidentiality of data while in transit A vulnerable application, running on a HTTPS site, can be hacked just as