
# CHAPTER 9

## FAQ Content Management System

If you attend any reasonably large IT conference, one of the buzzwords you are likely to hear tossed around the shop floor is content management. The buzzword and its vehicle of choice, the Content Management System (CMS), refer to Web applications that provide a simple and effective means of managing content.

Building a CMS is not a walk in the park. The major challenge that you face is in presenting all of the necessary tools needed to manage the content in a way that is simple but comprehensive. Many CMSs also deal with different types of users (admins, normal users, moderators, and so on), so you also need to provide a secure and consistent permissions system.

In this chapter, you carefully step over the fear and doubt, and take the challenge head on. Prepare yourselves to build a fully buzzword-compliant CMS.

### NOTE

#### Learn by Doing It Wrong

The project in this chapter was one that I developed some years ago as an independent CMS. Although I released the code on the Internet in an alpha state, the project was largely unfinished and still needed additional work to complete the application.

While preparing for this chapter, I took the original code, corrected it, and completed it. This process involved fixing all of the nasty nested tables and other bad programming habits that I picked up while learning PHP. Although fixing the code involved practically rewriting it, the process was a satisfying example of the progress I made since the project was originally written.

I recommend you regularly revisit your old projects and give them a spring-cleaning. If nothing else, it will provide a satisfying reminder of the progress you are making in your development.

### PROJECT OVERVIEW

In this chapter, you will create a CMS for Frequently Asked Questions (FAQ) lists. The questions are typically displayed as links, which in turn display the answer to the question.

To get a better feel for the project, you first explore a number of use cases that better explain the different types of functionality:

Bill goes to the FAQ Web site and wants to find out more about PHP. When the site loads, he can see a list of subjects in the sidebar. One of the subjects is PHP, so Bill clicks the link and the page displays a list of topics that are part of the PHP subject. Bill then clicks one of the topics, variables, and a list of related questions is displayed, with a short summary of the answers. Bill chooses one of the questions; the page now displays the question, the answer, and some related comments. As he reads the question, Bill decides he would like to post a comment. He logs into the site with his username and password and then returns to the question. A form is now displayed under the comments, so Bill enters his thoughts into the form and submits it. The comment now appears on the page.

This use case demonstrates how a typical user can come to the site, browse the content, and add comments to a question. The sidebar acts as a mechanism to navigate between the subjects and topics, and the main content (the questions) is displayed on the body of the page.

To make the site as community-orientated as possible, users should be able to own a subject and manage how content is added to that subject:

Ade takes a look at the PHP subject information page on the Web site. The page displays who owns the subject, but he notes that it currently has no owner. Because Ade is currently logged in, a link appears that allows him to propose himself as a new owner for the subject. He clicks the link and is taken to a page where he can enter the reasons he should be chosen as the owner.

Later, the administrator logs in and reviews the list of submitted ownership requests. She views Ade's request and decides that Ade is a suitable owner. She accepts Ade's request, and an email indicating his successful application is sent to him automatically.

Another key use case describes how to add and remove content from the project:

Now that Ade is the new owner of the PHP subject, he can add topics and questions. When Ade logs in, the new subject appears in his Control Panel (a page with information about his account). Ade can now use the Add Topic and Add Questions page to add content to the subject.

While Bill is browsing the PHP subject, he can also add questions by clicking the Add Question link on the subject information page. When Bill submits a question, it is held for moderation so that either Ade or the administrator can allow it.

Ade logs into the site and looks at the questions held for moderation. Inside the page, he can view the question details, and accept or deny it. He clicks the Accept link to make the question live.

These use cases have identified the core feature requirements for the application. When you build, you might find it useful to reread these use cases to get a better idea of how the application should work.

### BUILDING THE DATABASE

The database you will create is shown in Figure 9-1.

The four core tables are subject, topics, questions, and comments. These related tables also look up with the users table, which stores user accounts. The mod_subowner table stores ownership requests.

#### Implementing the Database

Start phpMyAdmin. Create a new database called `faq` and add the following tables:

#### The admins Table

- `id`: Make this a `TINYINT` (few admins are necessary) and turn on `auto_increment`. Set this field as a primary key.
- `username`: Make this a `VARCHAR` with a length of 10.
- `password`: Make this a `VARCHAR` with a length of 10.

![](img/c75d0c4fa51711b62f211459ae794f3f_320_0.png)

**FIGURE 9-1** The relationship of content over four tables (subjects, topics, questions, comments) is similar to the forums project.

#### NOTE: Active and Inactive Questions

The *active* field lives inside the *questions* table. This field identifies whether the question is live. If the field contains 0, the question is currently being held for moderation. If the field is set to 1, the question is live.

When a user who does not own the subject submits a question, *active* is set to 0 (Requires moderation). When the owner adds a question, *active* is set to 1. When a question to be moderated is accepted, *active* is changed from 0 to 1.

#### The comments Table

- `id`: Make this a `BIGINT` (several comments are possible) and turn on `auto_increment` in the Extras column. Set this field as a primary key.
- `question_id`: Make this an `INT`.
- `title_id`: Make this a `VARCHAR` and set the size to 20.
- `comment`: Make this a `TEXT`.
- `user_id`: Make this an `INT`.
- For this table, select the `InnoDB` table type.

#### The mod_subowner Table

- `id`: Make this an `INT` (several requests are possible) and turn on `auto_increment`. Set this field as a primary key.
- `sub_id`: Make this an `INT`.
- `user_id`: Make this an `INT`.
- `reasons`: Make this a `TEXT`.

#### The questions Table

- `id`: Make this an `INT` (several questions are possible) and turn on `auto_increment`. Set this field as a primary key.
- `topic_id`: Make this an `INT`.
- `question`: Make this a `VARCHAR` with a length of 50.
- `answer`: Make this a `TEXT`.
- `addedby_id`: Make this an `INT`.
- `dateadded`: Make this a `DATETIME`.
- `active`: Make this a `TINYINT`.
- For this table, select the `InnoDB` table type.

#### The subjects Table

- `id`: Make this an `INT` (several subjects are possible) and turn on `auto_increment`. Set this field as a primary key.
- `subject`: Make this a `VARCHAR` with a length of 20.
- `blurb`: Make this a `TEXT`.
- `owner_id`: Make this an `INT`.
- For this table, select the `InnoDB` table type.

#### The topics Table

- `id`: Make this an `INT` (several topics are possible) and turn on `auto_increment`. Set this field as a primary key.
- `subject_id`: Make this an `INT`.
- `name`: Make this a `VARCHAR` with a length of 20.
- For this table, select the `InnoDB` table type.
