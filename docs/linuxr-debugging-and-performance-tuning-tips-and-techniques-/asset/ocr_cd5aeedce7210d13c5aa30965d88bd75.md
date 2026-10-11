The professor's program uses `mktemp()` to create temporary files, and the student, having in the past watched the grading program create and remove temporary files, has figured out the algorithm that `mktemp()` uses. (The GLIBC version doesn't have this problem, but not all systems use GLIBC!) Figure 12.2 illustrates the race condition and how the student takes advantage of it.

![](bbox=[0.078, 0.263, 0.81, 0.418])

# FIGURE 12.2
Race condition with `mktemp()`

Here's what happened.

+   1. The grading program uses `mktemp()` to generate a filename. Upon return from `mktemp()`, the race condition window is now open (line 19 in `ch12-mktemp.c`).

+   2. The kernel stops the grader so that other programs on the system can run. This happens before the call to `open()`.
+   
+   While the grader is stopped, the student creates the file with the same name `mktemp()` returned to the grader program. (Remember, the algorithm was easy to figure out.) The student creates the file with an extra link to it, so that when the grading program unlinks the file, it will still be available for perusal.

+   3. The grader program now opens the file and writes data to it. The student created the file with `~rw-rw-rw-` permissions, so this isn't a problem.

+   4. When the grader program is finished, it unlinks the temporary file. However, the student still has a copy. For example, there may be a profit opportunity to sell classmates their grades in advance.

Our example is simplistic; besides just stealing the grade data, a clever (if immoral) student might be able to *change* the data in place. If the professor doesn't double-check his program's results, no one would be the wiser.