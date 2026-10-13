
## Question 9

If you try opening the X Window over a network connection, and all you get is the following error, which of the following actions would you take?

```
cannot open display:0.0
```

- a. Use the reset command to clear the screen of display problems.
- b. Set the DISPLAY environment variable to localhost:0.0.
- c. Reconfigure your X Window settings.
- d. Use the XF86Setup utility to start the X Server.

Answer b is correct. This is the proper response to the error message, which directs the display locally. The reset command applies to a similar situation where you see pseudographics in a CLI simulating actual graphics. Because it is not directly related to any X Window functions, answer a is incorrect. Although reconfiguring your X Window settings might work with a tool like XF86Setup, it is not as easy a solution as setting the DISPLAY variable. Therefore, answer c is incorrect. Although starting the XF86Setup utility does start a generic X Server, you can't run any other programs in that X Server, which makes it less than useful in this case. Therefore, answer d is incorrect.

## Question 10

You're running different computers on the same e-commerce Web site. The computers are located in several different time zones to optimize data transfer speed with your customers. How would you synchronize the time between your computers? Hypothetically, assume you can set up a time server on a computer on your network at time.likemynetwork.com or on a remote network at time.asc.org.

- a. Set up an NTP time server on one of your computers. Set up each of your computers to synchronize time with your NTP server. Run the ntpdate time.asc.org command on each computer to complete the synchronization.
- b. Set up each of your computers to synchronize from a remote network. Run the ntpdate time.likemynetwork.com command on each of your computers to complete the synchronization.
- c. Set up an NTP time server on one of your computers. Set up each of your computers to synchronize time with your NTP server. Run the ntpdate time.likemynetwork.com command on each computer to complete the synchronization.
- d. Set up each of your computers to synchronize from a remote network. Run the ntpdate asc.org command on each of your computers to complete the synchronization.

Answer c is correct. If you set up an NTP time server on one of your computers, you need to apply the ntpdate command to that server. Answer a directs you to set up a local NTP server, and then directs the ntpdate command on a remote computer; therefore, answer a is incorrect. Because answer b directs you to synchronize from a remote network, and then apply the ntpdate command to a local computer, this solution won't work. Therefore, answer b is incorrect. Because answer d does not use ntpdate to contact the correct computer, answer d is also incorrect.

## Need to Know More?

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_301_0.png)

Johnson, Dwight. ed. SuSE Linux 6.0 Installation, Configuration and First Steps. SuSE GmbH, Nürnberg, Germany, 1998. This manual for S.u.S.E. Linux provides excellent descriptions of problems and potential solutions, which are applicable for all distributions.

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_301_1.png)

Welsh, Matt, Lar Kaufman, and Matthias Kalle Dalheimer. Running Linux. O'Reilly & Associates, Sebastopol, CA, 1999. ISBN 1-56592-469-X. Possibly the key resource book on the Linux operating system. Although much of the information in this book is based on older versions of Linux, the basic data is concise, well written, and applicable today. Much of the writing in this book is not suitable for the novice user. If you can understand the points in this book, you have a better chance of learning troubleshooting shortcuts quickly.

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_301_2.png)

If you want more information about time servers worldwide, review the www.eecis.udel.edu/~ntp Web site.

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_301_3.png)

Explore the Web site for the Linux Documentation Project at www.linuxdoc.org, which is the central repository for Linux manuals, HOWTOs, and a number of other book-length documents. Many HOWTOs include troubleshooting sections. One important HOWTO is Howard Mann's Online Troubleshooting Resources HOWTO.

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_301_4.png)

Another important document is the Linux System Administrators' Guide at www.tml.hut.fi/~viu/linux/sag. This guide is written for newer administrators. You can also find a copy of this guide through the Linux Documentation Project at www.linuxdoc.org.

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_302_0.png)

## Sample Test

This chapter provides pointers to help you develop a successful test-taking strategy. These helpful tips include how to choose proper answers, how to decode ambiguity, how to work within the Sair Linux/GNU testing framework, how to decide what you need to memorize, and how to prepare for the test. At the end of the chapter, I include 50 questions on subject matter pertinent to the Sair Linux/GNU Installation and Configuration Level 1 certification exam 3X0-101. In Chapter 16, you'll find the answer key to this test. Good luck!

## Questions, Questions, Questions

There should be no doubt in your mind that you are facing a test full of specific and pointed questions. Each exam includes 50 questions. You are allotted 60 minutes to complete the exam.

Remember, questions will belong to one of three basic types:

- Multiple choice with a single answer
- Multiple choice with multiple answers
- Statement with a choice of true or false

You should always take the time to read a question at least twice before selecting an answer. Not every question has only one answer; many questions require multiple answers. Therefore, you should read each question carefully, determine how many answers are necessary or possible, and look for additional hints or instructions when selecting answers.

## Choosing Proper Answers

Obviously, the only way to pass any exam is to select enough of the right answers to obtain a passing score. However, Sair's Linux exams are not standardized like the SAT and GRE exams; they are far more diabolical and convoluted. In some cases, questions are strangely worded, and deciphering them can be a real challenge. In those cases, you may need to rely on answer elimination skills. Almost always, at least one answer out of the possible choices for a question can be eliminated immediately because it matches one of the following conditions:

- The answer does not apply to the situation.
- The answer describes a nonexistent issue, an invalid option, or an imaginary state.
- The answer may be eliminated because of information in the question itself.

After you eliminate all answers that are obviously wrong, you can apply your retained knowledge to eliminate further answers. Look for items that sound correct but refer to actions, commands, or features that are not present or not available in the situation that the question describes. If you're still faced with a blind guess among two or more potentially correct answers, reread the question. Try to picture how each of the possible remaining answers would alter the situation. Be especially sensitive to terminology; sometimes the choice of words (remove instead of disable) can make the difference between a right answer and a wrong one.

Only when you've exhausted your ability to eliminate answers and remain unclear about which of the remaining possibilities is correct should you guess at an answer. An unanswered question offers you no points, but guessing gives you at least some chance of getting a question right. Just don't be too hasty when making a blind guess.

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_304_0.png)

> Because this is not an "adaptive" exam, you can wait until the last round of reviewing questions (just as you're about to run out of time or unanswered questions) before you start making guesses. Although guessing should be a last resort, you should answer every question. You don't lose any credit if you answer a question incorrectly.

## Decoding Ambiguity

Sair Linux/GNU exams have a reputation for including questions that can be difficult to interpret, are confusing, or are ambiguous. In my experience with numerous exams, I consider this reputation to be completely justified. The Sair Linux/GNU exams are tough, and they're deliberately made that way.

The only way to beat Sair at its own game is to be prepared. You'll discover that many exam questions test your knowledge of things that are not directly related to the issue raised by a question. This means that the answers you must choose from, even incorrect ones, are just as much a part of the skill assessment as the question itself. In other words, the more you know about the operating system, the easier it is for you to tell right from wrong.

Questions often give away their answers, but you have to be Sherlock Holmes to see the clues. Often, subtle hints appear in the question text in such a way that they seem almost irrelevant to the situation. You must realize that each question is a test unto itself, and that you need to inspect and successfully navigate each question to pass the exam. Look for small clues, such as the mention of times, group permissions and names, and configuration settings. Little things such as these can point to the right answer if they're properly understood; if missed, they can leave you facing a blind guess.

Another common difficulty with certification exams is vocabulary. You may see some utilities and features named in obvious ways in some cases and completely inanely in other instances. Be sure to brush up on the key terms presented at the beginning of each chapter of this book. You may also want to read the glossary at the end of this book the day before you take the test.
