# Jade — James' DSSL Engine 123

```
$ jockmeier@thor:/files/Download$ cp cp.jade-1.2.1.tar.gz /tmp/
$ jockmeier@thor:/files/Download$ cd /tmp/
$ jockmeier@thor:/tmp$ tar -xzf jade-1.2.1.tar.gz
$ jockmeier@thor:/tmp$ cd jade-1.2.1
$ jockmeier@thor:/tmp/jade-1.2.1 ./configure
```

![](bbox=[0.075, 0.068, 0.738, 0.497])

In a Zip format, so you create a Jade directory under the Program Files directory and unzip the files in that directory.

# Using Jade

Generally, you don't use Jade by itself. Instead, Jade is called from other programs. However, you can use Jade to produce a few types of output directly from the command line.

To produce an RTF file with Jade from the command line, as shown in Figure 6.4, try this:

```
jade inputfile.sgml -t rtf -o outputfile.rtf
```

If Jade is installed properly, and your document is relatively free of errors, you should have an RTF file from the DocBook file.

To create a TeX file from your DocBook document, as shown in Figure 6.5, use the following:

```
jade inputfile.sgml -t tex -o outputfile.rtf
```