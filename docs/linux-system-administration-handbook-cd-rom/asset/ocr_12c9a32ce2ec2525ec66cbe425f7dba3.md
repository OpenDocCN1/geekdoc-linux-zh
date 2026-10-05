# 14.4 Python

Last, I have my CGI work. Most of the work on our Web site is on our internal network (some call it an intranet). This allows us to have a common repository for information—how the phones work, what drive letters which NFS mount, even schedules listing when people will be out of the office. This last one requires the CGI work. I have a SQL database program called PostgreSQL (which you got!) has a Perl interface. Perl also has a CGI interface, so I can build my form and CGI script all into one compact (under 200 lines) file. In one instance, a user can enter their name, what day they'll be out, and why they'll be out. This information then gets entered into the database. In another form, a person can enter data and query the database.

Perl over other languages? I've known Perl for a few years and got to use how quickly you can write a program and get it working. Plus you don't have to worry about the memory, pointers, includes files, and compiler problems that seem to be in C. I wouldn't want to write anything big in it, but my job typically doesn't require large programs. They're mostly small programs, and probably smaller in terms of line count than a comparable C program. Why not Perl or another language? I don't need the OOP that Python provides. Other scripting languages (like sh or csh) have all the functionality built into Perl already, but has the form of a real language and is something I'm much more used to, coming from my Pascal and M days.

# 14.4 Python^2

```
http://www.python.org
```

Now, unlike Mark, at half of my job is CGI programming and irony-fact, I don't use Perl. I ironically since anyone who has looked into doing CGI programming has undoubtedly noticed that most of it is done in Perl. In fact, it can be difficult to find a book that concentrates on writing CGI in any other language, but they are rumored to exist.

I used to be a huge Perl fan, but I didn't know any better then. I was actu-just happy to be writing CGI. I discovered Python on my way near the end of my tenure in grad school and wanted to learn it, but never really had the time or didn't think I did. Finally, about six months and two years later decided to finally learn another language. I really wasn't happy with Perl, I

> ^Written by Cary