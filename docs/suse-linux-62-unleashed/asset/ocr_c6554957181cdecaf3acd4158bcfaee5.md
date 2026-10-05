"[T]he three great virtues of a programmer: laziness, impatience, and hubris."
Wall and Schwartz, in Programming Perl

Automation enlists a machine—a Linux computer, in this case—to perform jobs automatically. However, the key to successful automation, and the true subject of this chapter, is attitude. The most important step you can take in understanding mechanisms of automation under SuSE Linux is to adopt the attitude that the computer works for you. For example, when you wonder why you are typing a telephone number that the machine should already know, or you do not want to wait until midnight to start backups, you have taken the first step toward correctly applying automation techniques. This chapter offers more than a dozen examples of how small, understandable automation initiatives make an immediate difference. Let them lead you to your own successes.

# # First Example—Automating Data Entry

How can the details work out? Look at an example from the day before I started to write this chapter.

# # Problem and Solution

A client wanted to enhance an online catalog by including thumbnail pictures of merchandise for sale. After a bit of confusion about what this really meant, I realized that I needed to update a simple database table of products to include a new column (or attribute) that would specify the filename of the thumbnail for each item. The database management system has a couple of interactive (graphical) front ends, and I’m a swift typist, so it probably would have been quickest to point and click my way through the 200 picture updates. Did I? Of course not—what happened later demonstrates the wisdom of this decision. Instead, I wrote a shell script to automate this database update; it automatically sends the correct SQL statements to the database to add the column, and is shown in Listing 22.1.

LISTING 22.1 Shell Script That Updates a Database

```
# picture names seem to look like ($DIR/137-13p.jpg,
#$DIR/201-942f.jpg,...)
# The corresponding products appear to be {137-13P, 201-942F, ...}
DIR=/particular/directory/for/my/client

# Will we use .gif-also, eventually? I don't know.
for F in $DIR/*.jpg
```