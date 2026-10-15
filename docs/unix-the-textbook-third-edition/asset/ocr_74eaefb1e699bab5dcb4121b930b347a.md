In the UNIX system, the crypt command can be used to encrypt and decrypt files that the user wants to keep secret. The techniques for converting an encrypted file back to original are well known. However, the average user is not familiar with these techniques, so the use of crypt results in a fairly good scheme for protecting files. If your work requires higher-level secure documentation and communication, you should use the openssl and crypto tools.

# QUESTIONS AND PROBLEMS

+   1. List five file-processing operations that you consider advanced.
+   2. What are regular expressions? What do the following regular expressions specify?
+      a. a|bc*
+      b. (a|b)*
+      c. a|(b*)c+
+   3. Give the vi command for replacing all occurrences of the string DOS with the string UNIX in the whole document that is currently being edited. What are the commands for replacing all occurrences of the strings DOS and Windows with the string UNIX from the lines that start or end with these strings in the document being edited?
+   4. Give the vi command for deleting all four-letter words starting with B, F, b, and f in the file being edited.
+   5. Give the vi command for renaming all C source files in a document to C++ source code files. Note: C source files end with .c and C++ source files end with .cpp.
+   6. What is file compression? What do the terms compressed files and decompressed files mean? What commands are available for performing compression and decompression in UNIX? Which are the preferred commands? Why?
+   7. Take three large files in your directory structure—a text file, a PostScript file, and a picture file—and compress them by using the compress command. Which file was compressed the most? What was the percentage reduction in file size? Compress the same files by using the gzip command. Which resulted in better compression, compress or gzip? Uncompress the files by using uncompress and gunzip commands. Show your work.
+   8. What is sorting? Give an example to illustrate your answer. Name four applications of sorting. Name the UNIX utility that can be used to perform sorting.
+   9. Go to http://cnn.com/weather and record the high and low temperatures for the following majors cities in Asia: Kuala Lumpur, Karachi, Tokyo, Lahore, Manila, New Delhi, and Jakarta. In a file called asiapac.temps, construct an ASCII table comprising one line per city in the order: city name, high temperature, and low temperature.