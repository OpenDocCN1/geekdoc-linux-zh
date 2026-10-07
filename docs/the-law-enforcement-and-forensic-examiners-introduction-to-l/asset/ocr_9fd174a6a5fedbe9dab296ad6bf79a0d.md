# v.4.33 A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

+   - aim forensic imaging tool provided primarily to create images in the Advanced Forensic Format (AFF).

This is not an exhaustive list. These, however, are some of the most commonly used (as far as I know). We will cover dc3dd, ewfacquire, and ddrescue in this document.

# dc3dd

The first alternative imaging tool we will cover is dc3dd. Imaging is tool based on original (patched) code from dd. It is very similar to the popular dcflldd but provides a slightly different set. My choice of cover either dcflldd or dc3dd is largely arbitrary. dc3dd is maintained by DoD (Department of Defense) Cyber Crime Center Regardless of which (dc3dd or dcflldd) you prefer, familiarity with one of these tools will translate nearly to the other with some reading and experimentation, as they are very similar. While there are significant differences, many of the features we discuss in this section are common to both dc3dd and dcflldd.

The source package and more information for dc3dd can be found at https://sourceforge.net/projects/dc3dd/.

dc3dd is installed by default on a current versions of Slack. If you are using a different distribution, check your package manager's repository.

The page for dc3dd is easy to read. All the information you need to use the advanced features of this imaging tool are nearly laid out for you.

Let's have a look at the basic usage of dc3dd. As you read through the usage section of the man page, you will notice a few additions to regular dd for the forensic examiner. Let's consider these notable notations:

| hof=FILE or DEVICE | hash the output file: Similar to the of= parameter for dd, this writes the specified output file and hashes and verifies the output bytes as. This essentially takes the place of hashing your image with sha1sum and md5sum it completes. |
| of=BASE.FMT | split the output file: Split the output file, and use the name BASE and specify the file extension for each split file using FMT. This format can be numerical or alphabetical, and you can specify the length by the number of characters you include in FMT. |
| hof=BASE.FMT | hash and split the output file: This is essentially a combination of the first two parameters above. |

> dcfldd is also named for a DoD entity – the Defense Computer Forensics Lab.

106