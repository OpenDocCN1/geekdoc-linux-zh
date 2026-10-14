# METHOD #1

Lynx
DEB: lynx
RPM: lynx
WWW: http://lynx.browser.org/

You can view an image on the Web by giving the URL of the image as an argument to lynx (see Recipe 33.2 [Using Lynx], page 643). The image will be displayed with whatever "helper" application is set up to show images via lynx.

⇒ To view the image at the URL ftp://garbo.uwasa.fi/garbo-gifs/garbo01.gif, type:
$ lynx ftp://garbo.uwasa.fi/garbo-gifs/garbo01.gif [RET]

NOTES: This method only works in X.

You could also give the URL for the image as an argument in this way to some other browser, such as Mozilla (see Recipe 33.1 [Using Mozilla], page 638).

# METHOD #2

ImageMagick
DEB: imagemagick
RPM: ImageMagick
WWW: http://www.imagemagick.org/

Libwww-perl
DEB: libwww-perl
RPM: perl-libwww
WWW: http://ftp.ics.uci.edu/pub/websoft/libwww-perl/

If you just want to view an image file from the Web, you don't have to use a Web browser at all—instead, you can use display, giving the URL you want to view as an argument. It uses GET (sometimes get), part of the libwww-perl package, to fetch the URL.

This method is especially nice for viewing your favorite webcam image, for viewing images on FTP sites, or for putting in scripts—you don't have to start a browser, log in, or type any other commands at all.