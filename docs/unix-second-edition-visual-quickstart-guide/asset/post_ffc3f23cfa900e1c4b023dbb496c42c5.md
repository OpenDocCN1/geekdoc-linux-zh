
# Decoding Files
with uudecode

You’ll decode files whenever you receive binary files through email—it’s the only way you can use encoded files. Although most email programs and news readers will take care of decoding files for you (and, therefore, you won’t need the information here), you may need to do it manually on occasion. (Hint: If you open up a file or an email message and see something like Code Listing 13.3, you’ve got a little decoding to do. To avoid the gibberish, decode your files, as shown in Code Listing 13.4.

## To decode files with uudecode:

- uudecode rowboat.uue

At the shell prompt, type uudecode followed by the name of the file to decode (Code Listing 13.4).

```
[ejr@hobbes compression]$ uudecode rowboat.uue
[ejr@hobbes compression]$ ls -l row*
-rw-r--r-- 1 ejr users 128886 Jul 27
+ 09:52 rowboat.jpg
-rw-r--r-- 1 ejr users 177606 Jul 27
+ 09:51 rowboat.uue
[ejr@hobbes compression]$
```

Code Listing 13.4 Udecoding files is straightforward.

## Tips

- When you receive an encoded file, you might have to uncompress or unzip it in addition to decoding it. See the appropriate sections later in this chapter for details.

- If you have a file that you suspect is unencoded, use head plus the filename to view the top ten lines of the file. If it’s really uuenencoded, you’ll see a line saying so at the top, as shown in Code Listing 13.3. The 644 in the list is the file’s permissions, and rowboat.jpg is the filename that the extracted file will have. See Chapter 5 for highly interesting details about file permissions.

```
[ejr@hobbes compression]$ head rowboat.uue
begin 644 rowboat.jpg
M"C"=6H<"E"(C"B"C"E"C"E"C"E"C"E"C"E"C"E"C"E"C"E"C"E"C"E"C"
MC"#4FKN3JCKS.25Q0IFJR=SN97,A*H"B1J9B1Y;B4G-F46;FJT]"1A
M@GQ;V8R&AE"-O,:ST;GJN"IY,W4G-F48"XRR"1Q98IT,S4B";J8EVEP
M:7IA-4H*"B14-6AE;VYL-2IR9K6L;D9VJ09"1P;8S21T;R18-7DP
M;SM8FRS(&ST"G5E-10F-FA6-VAE-F4-BAE(AQU);G-E@1B7,9@GR
M9G0D;V18B6SN(&U-1A;F08W17B-H6@0-6;G9T1P7?G-6W-8AE-6@0
MFTB;V8P6SR,FET-7J-E;IF:6Y1-VA3"P8B6YD"C"U"-11;G-1984@F]X
M97,N"B*"C"@"E"C"@"E"C"@"M2i5879E($J$A)G"Y";B5AE(K1A;6EN
M8R1O98IT,B44V-R97-B*H"HB1E6S8V;E7,-6,8;7556;6-VAA-"1%
[ejr@hobbes compression]$
```

Code Listing 13.3 Use the head command to view the top of a file. The "begin" line is the tipoff that it’s a uuenencoded file, with 644 permissions and the name of rowboat.jpg.

# Archiving with tar

Occasionally, you’ll want to take a bunch of files and make them into one file, such as when you’re archiving information, for example. You might think of it as tossing a bunch of toys into a toy box—that is, taking a bunch of related things and storing them all in one place.

Using tar (which came from “tape archive”), you can take a bunch of files and store them as a single, uncompressed file (see Code Listing 13.5). You’ll use tar files not only to store information, but also to create a single source for compressing and gzipping files, which are discussed later in this chapter.

```
[ejr@hobbes compression]$ ls -l
total 2290
drwxrwxr-x  2 ejr users  1824 Jul 23 10:56 Feather
drwxrwxr-x  2 ejr users  1824 Jul 23 10:49 Zipodeedoodah
-rw-rw-r-- 1 ejr users  53678 Jul 23 06:42 bigfile.gz
-rw-rw-r-- 1 ejr users  53678 Jul 23 10:16 bigfile.new.gz
-rw-rw-r-- 1 ejr users  73989 Jul 23 10:16 bigfile.uu
-rw-rw-r-- 1 ejr users  128886 Jul 23 11:45 file1.htm
-rw-rw-r-- 1 ejr users  128886 Jul 23 11:45 file2.html
-rw-rw-r-- 1 ejr users  686080 Jul 23 10:41 folder.tar
-rw-rw-r-- 1 ejr users  268156 Jul 23 06:53 folder.zip
-rw-rw-r-- 1 ejr users  128886 Jul 23 06:37 fountains1.txt
-rw-rw-r-- 1 ejr users  55124 Jul 23 06:38 fortunes1.zip
-rw-rw-r-- 1 ejr users  0 Jul 23 11:21 gzip
-rw-rw-r-- 1 ejr users  73978 Jul 23 11:15 home.gz.uu
-rw-rw-r-- 1 ejr users  177607 Jul 27 09:34 house.uu
-rw-rw-r-- 1 ejr users  53792 Jul 23 06:52 newzip.zip
-rw-rw-r-- 1 ejr users  128886 Jul 23 08:19 ournewhouse.jpg
-rw-rw-r-- 1 ejr users  128886 Jul 27 09:52 rowboat.jpg
-rw-rw-r-- 1 ejr users  177686 Jul 27 09:51 rowboat.uu
drwxrwxr-x  3 ejr users  1024 Jul 23 12:56 temp
[ejr@hobbes compression]$ tar -cf tarredfilename.tar Feather
[ejr@hobbes compression]$
```

Code Listing 13.5 Tarring files binds them all together into a single file.
