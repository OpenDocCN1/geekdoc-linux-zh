After running this script, you should perform a quick check to make sure everything is as it should be. In case of a problem, you can rename the current production directory to something else, and change the staging directory name back to your production directory name to restore your last production site.

# Building a Web Site by Using Templates and makepage

Maintaining a strict Web cycle provides you with a repeatable process for publishing great Web sites. However, you still need a content presentation process that is highly automated and requires very little human interaction.

Many expensive software programs claim to help in the process. Some people use Microsoft Front Page to manage content development; some use Dreamweaver; some use other products. Some people use more robust methods from Web development companies that cost hundreds of thousands of dollars. What follows is a solution that works for me (and has for years) in maintaining Web sites ranging from a few pages to few hundred pages in size. The requirements for this solution are:

+   ◆ Create a simple mechanism for content authors to publish Web pages with consistent look and feel.
+   
+   ◆ Require the least amount of work on the content author's part so that most of the work is automated.
+   
+   ◆ Assume that the content developer knows very little HTML and prefers to submit contents in text format.

To implement such a solution, I wrote *makepage*, a script that is included on this book's CD-ROM. This script uses a set of HTML templates and a body text (contents) page to build each page on the Web site. When I started this project, I wanted to generate each page on-the-fly by using CGI or mod_perl, but I later decided to generate the contents once a day because my sites were being updated only once or twice a day. However, it is extremely easy to increase the frequency of the update, as you learn in this section. The *makepage* script assumes that each page consists of:

+   ◆ A left navigation bar
+   
+   ◆ A right navigation bar
+   
+   ◆ A bottom navigation menu
+   
+   ◆ A body area that houses the contents of a page

Whenever the *makepage* script is run on a given directory, it looks for all the files ending with .txt extension and creates corresponding .html pages. For example, if you run the *makepage* script in a directory with a text file called *index.txt*, the script will run and produce output similar to this: