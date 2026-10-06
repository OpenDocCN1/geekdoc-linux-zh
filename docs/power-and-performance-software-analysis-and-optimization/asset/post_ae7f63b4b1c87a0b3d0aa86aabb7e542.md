
## 4.5 Step 4: Check upstream

modes of communication utilized by many projects. These typically are mailing lists, bug trackers, and IRC channels. The links to these, or the desired communication method, along with any guidelines for their usage, can typically be found on the project's website.

Here are some tips for getting results:

- 1. Check the project's mailing list archives and bug tracker to see whether the issue reported is already known. If so, use this information to determine what further steps should be taken.

- 2. Since each community is unique, the author finds it helpful to examine prior communications, such as the mailing list archive, in order to gain a better understanding of the community and how it operates. If archived communications are not available, or if achieved communicating via a real-time format, such as IRC, the same effect can be achieved by lurking on the channel asking your question. Taking the time to understand the community's dynamic will typically yield helpful insights on how to tailor your communication for getting results.

- 3. If communicating with mail, ensure that your email produces emails that adhere to your project requirements. When doubt, a safe configuration is the one described in the Linux kernel documentation, under |LINUX_SRC/Documentation/email-clients.txt.

- 4. Avoid HTML emails at all. mailing lists will reject HTML emails, and many developers, including the author, maintain `procmail` rules classifying all HTML as spam.

- 5. Avoid Top-Posting. Type your responses inline. This simplifies code reviews and makes it much easier to follow the conversation.

- 6. When possible, use `git send-mail` for emailing patches. It doesn't have to be perfect, but at least make an effort. Spelling and grammar reflect back on the writer's education and level of maturity.

- 7. Avoid attempting to communicate in a language other than the project's default. Some projects have special mailing lists or channels for different languages.

- 8. Verify your communications were received. If the mailing list is available, after sending an email, check to ensure that your email appears in the archive. If not immediately received, Sometimes emails require moderation before appearing, or perhaps the archives take a while to update. At the same time, mailing lists occasionally will drop.

- 9. Be polite. Remember, while many open source contributors are paid, many do so this as an enjoyable hobby. Keep in mind that no project or developer owes you anything,

- 10. Understand the terms of popular open source licenses, such as the GPL, LGPL, and BSD license. When in doubt, seek professional legal counsel.

- 11. Always unset or experimental code. The author typically prefers these communications with “RFC,” that is, Request For Comments.

- 13. Support your code. Just because your code has been accepted upstream doesn’t mean your job is over. When questions or bugs appear, take responsibility for your work.

- 14. Follow the project’s coding guidelines. This includes configuring your text editor for preferences such as spaces tabs or the number of characters in an indentation. This also includes following any formatting around bracket placement and spacing. When in doubt, follow the style of the existing code.

- 15. When submitting a patchset, ensure that every patch builds without later patches. Often when creating a series of interrelated patches, there are dependencies between the patches. This can lead to situations where one patch relies on something introduced in a later patch to compile. In this situation, the build is temporarily broken, but then immediately fixed by a later patch in the same patches. While this might not appear to be a problem, it becomes one whenever ever attempting to perform a bisection; see Section 4.5.3 for more information. Organize the patches so that any infrastructure is introduced before its use, and thus the tree will build after each patch.

## 4.5.3 WHAT

Obviously, what can be communicated depends on the progress made and the environment of the open source project. Some projects are very receptive to bug reports, while some projects aren’t interested in bug reports without patches.

This section will cover how to leverage some helpful features of Git in order to simple the work required to contribute.

## Git bisect

Tracking down a regression, performance or not, is much easier once the offending commit, that introduced the issue, is discovered. When reporting a regression, including this information can help accelerate the process of determining the next course of action. Git bisect makes this process simple through the git bisect command, performs a binary search on the commit range specified by the user. This search can interactively, with the user marking each commit suggested by Git as either good or bad, or automatically, with a script that communicates with Git via the exit status.

If not using Git, for some odd reason, there are two options. The first option is to leverage one of the existing tools that allows Git to interact with other SCM systems, such as git-svn. The second option is to use an equivalent tool or to manually perform the search of the commit history for the SCM system.

An interactive bisection session begins by executing git bisect start, which initializes some state in the .git directory of the repository. At any time, the history bisection commands can be printed by executing git bisect log, or looking at the file .git/BISE_LOG. It is possible to execute a list of bisect commands, such as t log file, via git bisect replay.

## 4.5 Step 4: Check upstream

At this point, Git expects the user to define the bounds for the search. This occurs by marking the first good commit, and the first bad commit, via the git bisect command. These commands take Git refs as arguments. Once both endpoints are marked, Git begins checking out individual commits. The user must then perform the required testing to determine whether the node suffers from the regression. If so, mark the commit as bad, using git bisect bad, or if not, mark the commit as good, using git bisect good. It is also possible to skip testing the current commit, via git bisect skip. This cycle will continue until the first commit is found. Git will print the SHA1 of this commit. Examining this commit should provide insight into what caused the regression. The bisection session can be terminated via git bisect reset, which will remove any bisection state, and return the tree to the original state from which the bisection was started.

The manual testing above can be alleviated by the use of git bisect run, which will execute a script and then use the return value to mark a given commit as good, a return value of 0, or bad, any return value between 1 and 127, excluding 125. The script returning a value of 125 indicates that the current couldn't be tested and should be skipped.

## Cleaning patches with git

A patch represents a logical change, expressed as the addition and subtraction of file lines, to a source tree. In the open source community, patches are the means of progress, so learning how to properly generate and structure patches is important for contributing.

Typically, the process of writing code is messy and imperfect. When submitting patches, the patches need to present the solution, not the process, in a logical and ordered manner. To accomplish this, the author keeps at least two branches for each endeavor, a development branch and a clean submission branch. The development branch will contain commits as progress is made, as adding new code or fixing types. The clean submission branch will rewrite the commit history of the development branch to separate the commits into logical changes. This can involve combining multiple commits into a single commit, removing unnecessary commits, editing commits and ensuring that the formatting complies with the project's formatting standards.

The author imagines that some readers are concerned by the concept of rewriting their commit history. Some of this concern stems from the fact that changing the commit history of a public branch is annoying to those who have based code on
