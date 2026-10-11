If it installs and runs properly, upload your source RPM to your favorite software repository, and you are finished.

If, regretably, you run into problems, RPM's build command accepts several options that enable you to step through the build process to identify and, hopefully, fix problems. The following list contains brief descriptions of the options:

+   - `-bp`—Validate the spec file's **prep** section

+   - `-bl`—Validate the file list in `%files`

+   - `-bc`—Perform a **prep** and **compile**

+   - `-bi`—Perform a **prep**, **compile**, and **install**

+   - `-bb`—Perform a **prep**, **compile**, **install**, and **build** only a binary package

+   - `--short-circuit`—Add this argument to skip straight to the specified build step (`p`, `l`, `c`, `i`, `b`)

+   - `--keep-temp`—Preserve the temporary files and scripts created during the build process

+   - `--test`—Perform a mock build to see what would be done (also performs `--keep-temp`)

After you resolve the errors, rebuild using `-ba`, upload your masterpiece, and wait for the kudos (and patches and bug fixes) to roll in.

# What's Next?

In this chapter, you looked at two different ways to distribute software, using tar, gzip, and install, and using the Red Hat Package Manager. This brings you to the end of the book. You have learned how to compile programs, covered many system programming topics, met many application programming interfaces, and briefly covered the huge subject of network programming. You were also introduced to a few essential programming utilities, such as RCS and gdd. To tie all these skills together, the next chapter walks you through building a music CD database.