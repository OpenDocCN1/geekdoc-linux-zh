# 4.5 Step 4: Check upstream

At this point, Git expects the user to define the bounds for the search. This occurs by marking the first good commit, and the first bad commit, via the git bisect good and git bisect bad commands. These commands take a list of Git refs as arguments. If both endpoints are marked, Git will return to HEAD, the current commit.

Once both endpoints are marked, Git will continue to out a commit to test, that is, the current node in the binary search. The user must then perform the required testing to determine whether or not the current node suffers from the same regression. If so, mark the commit as bad, using git bisect bad, or if not, mark the commit as good, using git bisect good. It is also possible to skip testing the current commit, via git bisect skip, or by manually removing the commit from the current tree, via git reset --hard HEAD-. Be aware that normal reset --hard HEAD will delete a commit from the branch. During bisection, once the bounds have been established and Git begins committing, Git checks out individual commits and deletes it from the original.

This cycle will continue until the first commit is found. Git will print the SHA1 of this commit, with the commit information. Examining this commit should provide insight into what caused the regression. The bisection session can be terminated via git bisect reset, which will remove any bisection state, and return the tree to the original state from which the bisection was started.

The manual testing above can be alleviated by the use of git bisect run, which will execute a script and then use the return value to mark a given commit as good, a return value of 0, or bad, any return value between 1 and 127, excluding 125. The script returning a value of 125 indicates that the current couldn't be tested and should be skipped.

# Cleaning patches with git

A patch represents a logical change, expressed as the addition and subtraction of file lines, to a source tree. In the open source community, patches are the means of progress, so learning how to properly generate and structure patches is important for contributing.

Typically, the process of writing code is messy and imperfect. When submitting patches, the patches need to present the solution, not the process, in a logical and ordered manner. To accomplish this, the author keeps at least two branches for each endeavor, a development branch and a clean submission branch. The development branch will contain commits as progress is made, as adding new code or fixing types. The clean submission branch will rewrite the commit history of the development branch to separate the commits into logical changes. This can involve combining multiple commits into a single commit, removing unnecessary commits, editing commits and ensuring that the formatting complies with the project's formatting standards.

The author imagines that some readers are concerned by the concept of rewriting their commit history. Some of this concern stems from the fact that changing the commit history of a public branch is annoying to those who have based code on