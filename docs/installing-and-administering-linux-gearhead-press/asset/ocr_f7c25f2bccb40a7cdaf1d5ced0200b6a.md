Table 7.2 lists some examples with explanations of common types of asterisk wildcard expansion.

Example 7.4 provides a couple of illustrations of normal asterisk wildcard expansion.

The exception to wildcard expansion is that there will *not* be a match to any files that begin with a single dot; that is, to any hidden files. Why not? The answer is, mostly for security reasons. Those files are intentionally hidden from prying eyes and fingers. They should not be exposed or even jeopardized by being included (perhaps innocently and inadvertently) to processes invoked by wildcard expansion, which introduces a certain lapse of user or administrator control. Also, if single-dot matches were allowed, the directories called `"."` and `".."` (that is, the current and parent directories, respectively) would also be fair game to whatever processes would be invoked. That could be very dangerous with certain commands (for example, rm).

Example 7.5 provides an example of the exception.

Now, wouldn't you know it—there are exceptions to the exceptions here. A match will be made to a single dot string if the single dot is included as part of the search string.

Example 7.6 provides an example to the “exception to the exception.”

These principles are easier to grasp through examples. Let’s look at Examples 7.4, 7.5, and 7.6. But first, those examples will be more meaningful if you take the time beforehand to create the following files with a text editor such as vi (be careful if you are not familiar with European-style phone numbers):

```
Filename: /home/gutiejuia/admin/phone##/RFL_Tel1

```

```
Madrid Head Office - +34 91 555 12 34
Travel Coordinator - Madrid - +34 91 555 00 01
Curate’s Office - +34 91 555 23 45
Barber/Surgery/MASH - +34 91 555 45 67
```