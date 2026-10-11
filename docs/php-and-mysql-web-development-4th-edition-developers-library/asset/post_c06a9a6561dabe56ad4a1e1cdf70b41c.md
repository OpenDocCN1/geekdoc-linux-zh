
### 1.2 A Sample Database

This section describes the sample database that we’ll use throughout the rest of this book. It provides a source of examples for you to try as you learn to put MySQL to work. We’ll draw examples primarily from two of the situations described earlier:

- The organizational secretary scenario. Our organization has these characteristics: It’s composed of people drawn together through an affinity for United States history (called, for lack of a better name, the U.S. Historical League). The members renew their membership periodically on a dues-paying basis. Dues go toward League expenses such as publication of a newsletter, “Chronicles of U.S. Past.” The League also operates a small Web site; it hasn’t been developed very much, but you’d like to change that.
- The grade-keeping scenario. You are a teacher who administers quizzes and tests during the grading period, records scores, and assigns grades. Afterward, you determine final grades, which you turn in to the school office along with an attendance summary.

Now let’s examine these situations more closely in terms of two requirements:

- You must decide what you want to get out of the database—that is, what goals you want to accomplish.
- You must figure out what you’re going to put into the database—that is, what data you will keep track of.

Perhaps it seems backward to think about what comes out of the database before considering what goes in. After all, you must enter your data before you can retrieve it. But the way you use a database is driven by your goals, and those are more closely associated with what you want to get from your database than with what you put into it. Presumably you’re not going to waste time and effort putting information into a database unless you plan to use it for something later.

#### 1.2.1 The U.S. Historical League

The scenario here is that you as League secretary maintain the membership list using a word processing document. That works reasonably well for generating a printed directory but limits what else you can do with the information. You have these objectives in mind:

- You want to produce output from the directory in different formats, using information appropriate to the application. One goal is to generate the printed directory each year—a requirement the League has had in the past that you plan to continue to carry out. You can think of other uses for the information in the directory, too—for example, to provide the current-member list for the printed program distributed to attendees of the League’s annual meeting. These applications involve different sets of information. The printed directory uses the entire contents of each member’s entry. For the meeting program, you need to pull out only member names (something that hasn’t been easy using a word processor).
- You want to search the directory for members who satisfy various criteria. For example, you want to know which members renew what memberships soon. Another application that involves keyword searches is from the list of keywords you maintain for each member. These keywords describe areas of U.S. history in which each member is particularly interested (for example, the Civil War, the Depression, civil rights, or the life of Thomas Jefferson). Members sometimes ask you for a list of other members with interests similar to their own, and you’d like to be able to satisfy these requests.
- You want to put the directory online at the League’s Web site. This would benefit both the members and yourself. If you can convert the directory to Web pages by some reasonably automated process, an online version of the directory would be always up to date, something not true of the printed version. And if the online directory can be made searchable, members could easily look for information themselves. For example, a member who wants to know which other members are interested in the Civil War could find that without waiting for you to perform the search, and you wouldn’t need to find the time to do it yourself.

I’m well aware that databases are not the most exciting things in the world, so I’m not about to make any wild claims that using one stimulates creative thinking. Nevertheless, when you stop thinking of information as something you must wrestle with (as you do when using your word processing document) and begin thinking of it as something you can manipulate relatively easily (as you hope to do with MySQL), it has a certain liberating effect on your ability to come up with new ways to use that information:

- If the information in the database can be moved to the Web site in the form of an online directory, you might also be able to make information flow the other way. Suppose that members could edit their own entries online to provide updates for the database. Then you wouldn’t have to do all the editing yourself, and it would make the information in the directory more accurate. You’d really like to avoid doing all the directory editing yourself, but the society doesn’t have much of a budget, and hiring someone is out of the question.
- If you store email addresses in the database, you could use them to send email to members that haven’t updated their entries in a while. The messages could show members the current contents of their entry, ask them to review it, and indicate how to make any needed modifications using the facilities provided on the Web site.
- A database might help make the Web site more useful in ways not even related to the membership list. The League’s newsletter, “Chronicles of U.S. Past,” has a children’s section containing a history-based quiz in each issue. Some of the recent issues have focused on biographical facts about U.S. presidents. The Web site could have a children’s section, too, where the quizzes are put online. Perhaps this section could even be made interactive, by putting the information from which quizzes are drawn in the database and having the Web server query the database for questions to present to visitors.

**Well!** At this point the number of uses for the database that you’re coming up with make you realize you might be getting a little carried away. After pausing to come back down to earth, you start asking some practical questions:

- Is this a little ambitious? Won’t it be a lot of work to set this up?

Anything’s easier when you’re just thinking about it and not doing it. Of course, and I won’t pretend that all of these ideas are trivial to implement. Nevertheless, by the end of this book you’ll have done everything we’ve just outlined. Just keep one thing in mind: It’s not necessary to do everything all at once. We’ll break the job into pieces and tackle it a piece at a time.

- Can MySQL be used to accomplish all these goals?

No, it can’t, at least not by itself. For example, MySQL has no built-in Web-programming facilities. But you can combine MySQL with other tools that work with it to complement and extend its capabilities.

We’ll use the Perl scripting language and the Perl DBI (database interface) module to write scripts that access MySQL databases. Perl has excellent text-processing capabilities, which allow for manipulation of query results in a highly flexible manner to produce output in a variety of formats. For example, we can use Perl to generate the directory in Rich Text Format (RTF), which can be read by all kinds of word processors, and in HTML format for Web browsers.

We’ll also use PHP, another scripting language. PHP is particularly adapted to writing Web applications, and it interfaces easily with databases. This enables you to initiate MySQL queries from Web pages and to generate new pages that include the results of database queries. PHP can be used with several Web servers (including Apache, the most popular server in the world), making it easy to do things such as presenting a search form and displaying the results of the search.

MySQL integrates well with these tools and gives you the flexibility to choose how to combine them to achieve the ends you have in mind. You’re not locked into some all-in-one suite’s components that have highly touted “integration” capabilities but that actually work well only with each other.

- And, finally, the big question: How much will all this cost?

The League has a limited budget, after all.

This might surprise you, but it probably won’t cost anything. If you’re familiar with the usual ken of database systems, you know that they’re generally pretty pricey. By contrast, MySQL often can be used for free. Even in enterprise settings where you need guaranteed support and maintenance arrangements, MySQL is relatively inexpensive as database systems go. (Visit <http://www.mysql.com> for details.) The other tools
