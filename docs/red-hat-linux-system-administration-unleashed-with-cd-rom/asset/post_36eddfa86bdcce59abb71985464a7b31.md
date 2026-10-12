
This doesn't have anything to do with systems administration, of course, but it does serve to illustrate the need to periodically review and revise policy as situations change. It is always important to review policies to make sure that the reasons why you put them into place still exist and to make sure that the policies do not conflict with one another. Outdated or inconsistent policies are two easy ways to ensure that all of your published policies are challenged or ignored outright.

## Dealing with Interruptions

Interruptions from users are a fact of life for all systems administrators, and how you deal with these interruptions will affect how well you accomplish the multitude of tasks that you are required to perform. Interruptions in this context refer not only to people barging into your office and demanding your attention, but also to people who barrage you with email or phone calls asking questions or requesting help. There are a number of ways to minimize the effects of interruptions from users. This section looks at a few of them and discusses their merits and flaws so that you can develop a solution that works for your situation.

### The "My Door Is Always Open" Strategy

One of the mistakes that some new systems administrators make, especially if they come from a customer support background, is to make it a habit to drop whatever they are doing to deal with a request from a user, no matter how trivial the request. Although this may seem like a good way to establish good relations with your users, it usually ends up causing whatever projects the sysadmin is working on to be delayed. The sysadmin is then left in the unenviable position of having to explain to his or her boss that projects were delayed so that he or she could deal with an unscheduled interruption from a user. The lesson that this type of systems administrator has to learn is how to prioritize work so that important user-generated interruptions are dealt with in a timely manner and others are dealt with within the confines of project schedules and other constraints on their time. Not learning this lesson usually results in the systems administrator either losing his job for failure to complete projects on time or not advancing in his career for the same reason.

This does not mean that you should cut yourself off from your users. A systems administrator who will take a few minutes to help out a user in distress can gain an ally for life. It is simply important to let users know that if you are working on a higher priority project, their problem may have to wait. It is important for the systems administrator to remember that even if the problem takes thirty seconds to solve, the total time involved to deal with the interruption includes the time to listen to the user's problem, formulate a solution, explain the solution to the user, implement the solution, and then resume whatever you were doing when you were interrupted.

### The “Send Me an Email” Strategy

The other end of the spectrum is the systems administrator who never has time to deal with users and whose response to everything is to send them an email with the question or request. While this strategy might sound better than the previous one, it can result in a whole other set of problems. One of these problems is likely to be alienation from the system users, who start to feel that the administrator has no time for them. Just as being too accessible to users can be a problem, not being accessible enough to users can cause management to look critically at you and impair your ability to advance your career.

Although you will most likely have fewer problems meeting project deadlines, your user community will not be satisfied with the level of service they are receiving from you. Another problem with this strategy is that you may become inundated with so many requests via email that you will find that you are spending more time reading email than you are dealing with the user issues. Another factor to consider is that although email is a good way to communicate, it is often easier and less time consuming to meet with a user briefly to outline the parameters of the request and then to add the request to your schedule.

This avoids scenarios like the following:

- User Email 1: My mouse isn't working right.
- Admin Reply 1: Define not working right.
- User Email 2: When I start X, the middle mouse button doesn't work.
- Admin Reply 2: Did it work at some point in the past?
- User Email 3: I just received a new mouse. The old one didn't have 3 buttons.

If you demand that all interactions with your users be via email, you can see that you may spend significantly more time trying to extract information from them than would have been spent if you simply sat down with the user for a few minutes to discuss the problem.

### The “Scheduled Interrupt Time” Strategy

Since minimizing the impact of user interrupts is the goal we are trying to achieve, some systems administrators try to establish a time period during which users are allowed to interrupt them. Approaches that utilize this idea may work well for a time, especially if most of your user interrupts are trivial to deal with and you have a small user community. However, as that user community grows you will often find that you have to increase the amount of scheduled interrupt time to deal with the larger number of users. Another deficit to this approach of dealing with interrupts is that every user tends to think that his problem is an emergency and seeks your help outside of the time you have set aside. This tends to be
especially true of managers, who are under pressure to meet their own goals and deadlines. This can turn out to be very detrimental to your career because those people whose problems fall outside of your scheduled interrupt time may try to blame you for failure to meet their own deadlines.

## Minimizing Interruptions Through Training

One of the ways to try to minimize the number of interruptions you get from users is to provide training for them. The idea is to teach the users to be self sufficient for trivial tasks and only come to you when a true crisis arises. The following sections examine a few ideas related to training your user base that can be applied to help minimize the number of trivial interruptions.

### Training Your Users

Some of the most annoying users to deal with are those who come to you with questions that could have been answered with a little work on their part. An untrained user can eat up a significant portion of your time and the key to eliminating this is to get the user trained. There are many ways that you can approach the training issue, but here are some of the ways that I have found to be effective.

### Making Training Enjoyable

One way to approach training is to make it as appealing as possible to the users. This can be accomplished by keeping the training informal and providing an incentive to attend. For example, if your budget allows, you might sponsor a series of lunch meetings at which a class is given on a technical topic by yourself or one of your users. If you have a room where users can sit and listen to your training while enjoying lunch, they are often more receptive to attending. It is also useful if you can videotape these lunch training sessions, so that people unable to attend can view the training at a later date. If your budget doesn’t allow for buying the whole group lunch, you might provide them with soft drinks.

### Start a Training Library

Another training approach that may work for you is to start a library of training books and videotapes that users can check out at their convenience. To encourage users to use these resources, you might schedule some time each week during which you make yourself available to answer questions about the materials and do some one-on-one training. This approach works best if your users are motivated to learn already.

### A Systems Orientation Guide

At a minimum, it is a good idea to develop a systems orientation guide for your users. The systems orientation guide is a document that lays out for users such things as where to find items on your network and how to request new software, and describes the tools available that can make their jobs easier. A sample table of contents for a systems orientation guide might look something like this:

- I Meet Your Servers
  - A. The Intranet Web Server
  - B. Electronic Mail
  - C. Application Servers
- II Network Resources
  - A. Printers
  - B. Shared Filesystems
  - C. Specialized Hardware
    - 1. Scanners
    - 2. CD-R Burners
- III Systems Administration Information
  - A. Acceptable Use Policy
  - B. Utilizing the Help Desk
  - C. Training Materials Available

This document does not have to be very long, but by providing a quick reference for your users that describes these items and how to make use of them, you can save yourself from having to answer these types of questions for every new employee. You could publish this information on the company intranet Web server, but for the new employee, it is often better to provide a paper copy so that they know where to look to find that Web server.

## A Combination Approach to User Interaction

The approach to dealing with user interrupts that may work for many situations is to combine the three approaches already discussed. The suggested combination is to plan for some amount of interruption time when making your deadlines with a margin to deal with emergencies and to provide a communications mechanism that is a combination of email and face-to-face communications. For example, you might plan on spending a couple of hours a week training your users on Linux and on the resources available on your network. By providing this training, you will reduce the number of trivial interrupts that occur and improve the productivity of the user as well as your own. Another suggestion is to make it a
