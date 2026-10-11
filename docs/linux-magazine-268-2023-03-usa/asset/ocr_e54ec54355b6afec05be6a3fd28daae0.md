![](bbox=[0.07, 0.07, 0.63, 0.27])

# Figure 1: How much Minuimus can shrink a file varies: These two files were reduced to 88 and 99 percent of their original sizes, respectively.

number of other programs, including AdvanceCOMP [3] for compressing specific file types, OptiPNG [4] for compressing PNG images, Jpegoptim [5] for compressing JPEG files, Gifscicle [6] and flexiGIF [7] for compressing GIF files, and Qpdf Tools [8] for converting PDFs.

It is difficult to predict how much Minuimus will shrink your PDFs. It depends on several factors, including primarily how effective the original program was at creating the PDF file in question and how much reduction potential is left for Minuimus. If the PDF file only consists of text, there is little potential for file size reduction. The situation is different if the PDF contains many graphics and images, because they usually offer plenty of downsizing potential.

Another program similar to Minuimus is Leanify [9]. If Leanify exists on your computer, Minuimus will also use it as a helper; the two programs complement each other with their capabilities. This combination gives you even better results.

By default, Minuimus is lossless: It does not reduce the quality of images in the PDF file, but simply optimizes the compression. However, a slight loss of quality is sometimes acceptable if it

results in smaller files. The following command

```bash
minuimus.pl --jpg-web FILE.pdf
```

converts the JPEGs in the document to the leaner WebP format, reducing the quality of the images to 90 percent.

# Minuimus in Use

After installation, call Minuimus with the command:

```bash
minuimus.pl FILE.pdf
```

I first tested Minuimus on the December 2022 community edition of LinuxUser (a German magazine) [10]. As shown in Figure 1, the file size was reduced from 12.7 to 11.2MB (about 88 percent of the original size). A loss of quality was not noticeable, especially with the images. The original metadata were also preserved.

When I compressed the e-paper with the full version of the December 2022 issue of LinuxUser, the results were similar. Minuimus reduced the size of the PDF from 32.8 to 28.7MB (87.5 percent of the original size). I also tried out Minuimus on a scan from the Internet Archive of Arthur Conan Doyle’s famous 1902 Sherlock Holmes novel The Hound of the

Baskervilles [11]. In this instance, Minuimus only managed to reduce the file size to just under 99 percent of the original (12.3 to 12.1MB). Compared to this, Minuimus shrank a book I had scanned myself from 82.7 to 66.9MB (about 81 percent of the original size). Figure 2 shows the results for all four tests.

# Conclusions

Installing Minuimus was uncomplicated, and it was easy to use with shell commands. I did manage to reduce the size of a number of files, but with varying degrees of success. The results depend on several factors, not least how much potential a PDF file has for reducing file size in the first place. Ultimately, every little bit helps when it comes to freeing up disk space. ☐☐

# Info

+   1. Minuimus: https://birds-are-nice.my/ software/minimus.html
+   2. Minuimus download: https://birds-are-nice.my/software/ minuimus.zip
+   3. AdvanceCOMP: http://www. advancecomme.fr/compr-readme
+   4. OptiPNG: https://optipng.sourceforge.net/
+   5. Jpegoptim: https://github.com/tjko/pegoptim
+   6. Gifscicle: https://www.lcdf.org/ gifscicle/
+   7. flexiGIF: https://create.stephan-brumme.com/ flexigif-lossless-gif-zw-optimization/
+   8. Qpdf Tools: https://github.com/ silas35/qpdftools
+   9. Leanify: https://github.com/JayKon/Leanify
+   10. LinuxUser 12/2022 Community Edition: https://www.linux-community. de/wp-content/uploads/2022/12/ lu-ce_2022-12.pdf
+   11. The Hound of the Baskervilles from the Internet Archive: https://archive.org/details/ houndofbaskervil100doyloaft/

![](bbox=[0.07, 0.82, 0.63, 0.88])

# Figure 2: Minuimus’ results depend on various factors and turn out differently every time. Here you can see the file sizes before and after processing for the four tests.