# ## PROJECT OVERVIEW

In this chapter, you will create a CMS for Frequently Asked Questions (FAQ) lists. The questions are typically displayed as links, which in turn display the answer to the question.

To get a better feel for the project, you first explore a number of use cases that better explain the different types of functionality:

Bill goes to the FAQ Web site and wants to find out more about PHP. When the site loads, he can see a list of subjects in the sidebar. One of the subjects is PHP, so Bill clicks the link and the page displays a list of topics that are part of the PHP subject. Bill then clicks one of the topics, variables, and a list of related questions is displayed, with a short summary of the answers. Bill chooses one of the questions; the page now displays the question, the answer, and some related comments. As he reads the question, Bill decides he would like to post a comment. He logs into the site with his username and password and then returns to the question. A form is now displayed under the comments, so Bill enters his thoughts into the form and submits it. The comment now appears on the page.

This use case demonstrates how a typical user can come to the site, browse the content, and add comments to a question. The sidebar acts as a mechanism to navigate between the subjects and topics, and the main content (the questions) is displayed on the body of the page.

To make the site as community-orientated as possible, users should be able to own a subject and manage how content is added to that subject:

Ade takes a look at the PHP subject information page on the Web site. The page displays who owns the subject, but he notes that it currently has no owner. Because Ade is currently logged in, a link appears that allows him to propose himself as a new owner for the subject. He clicks the link and is taken to a page where he can enter the reasons he should be chosen as the owner.

Later, the administrator logs in and reviews the list of submitted ownership requests. She views Ade's request and decides that Ade is a suitable owner. She accepts Ade's request, and an email indicating his successful application is sent to him automatically.