# 15.3 Is All That Paging Bad for My System?

Although we stated earlier that it may be normal to have high paging and scan rates, it is likely that the page scanner will be putting too much pressure on your application’s private process memory. If we scan at a rate of several hundred pages or more per second, then the amount of time that the page scanner takes to check whether a page has been accessed falls to a few seconds. This means that any pages that have not been used in the last few seconds will be taken by the page scanner when you are using the file system. This behavior can negatively affect application performance and is the reason why _priority paging_ was introduced.

If your system seems slow while the file system I/O is going on, it’s because your applications are being paged in and out as a direct result of the file system activity.

For example, consider an OLTP application that makes heavy use of the file system. The database is generating file system I/O, making the page scanner actively steal pages from the system. The user of the OLTP application has paused for 15 seconds to read the contents of a screen from the last transaction. During this time, the page scanner has found that those pages associated with the user application have not been referenced and makes them available for stealing. The pages are stolen, and when the user types the next keystroke, the user is forced to wait until the application is paged back in—usually several seconds. Our user is forced to wait for an application to page in from the swap device, even though the application is running on a system with sufficient memory to keep all of the application in physical memory!

The priority paging algorithm effectively places a boundary around the file cache so that file system I/O does not cause unnecessary paging of applications. The algorithm prioritizes the different types of pages in the page cache, in order of importance:

+   - Highest — Pages associated with executables and shared libraries, including application process memory (anonymous memory)
+   - Lowest — Regular file cache pages

When the dynamic page cache grows to the point where free memory falls to almost zero, the page scanner wakes up and begins scanning, but as long as the system has sufficient memory, the scanner only steals pages associated with regular files. The file system effectively pages against itself rather than against everything else on the system.

Should there be a real memory shortage where there is insufficient memory for the applications and kernel, the scanner is again allowed to steal pages from the applications. By default, priority paging is disabled. It is likely to be enabled by default in a Solaris release subsequent to Solaris 7. To use priority paging, you will