# # Installing AIDE

AIDE is a filesystem integrity-checking tool offering many of the features you'd expect from such a program. More information on AIDE, including links to download, are available at http://www.cs.tu.tz.fi/~rammer/aide.html and http://sourceforge.net/projects/aide.

After its downloaded, AIDE needs to be compiled. However, you will probably also need some prerequisites before attempting to compile AIDE. If this is the case, the configure script for AIDE will inform you of these prerequisites, which you will then need to download and compile before continuing with AIDE's compilation. One such prerequisite commonly needed is the mhash library. The mhash library can be downloaded from http://sourceforge.net/projects/mhash/

The mhash library should be compiled statically for use with AIDE. Follow the normal steps for unarchiving and compiling a software package:

```
```
tar -zxvf mhash-<NNNN>.tar.gz
cd mhash-<NNNN>
```
```

I recommend these compile options for the configure script:

```
```
./configure --prefix=/usr --enable-static=yes
```
```

After mhash has been configured, compile and install it with these commands:

```
```
make
make install
```
```

Compiling AIDE follows the same pattern as other software compilation, such as this in Linux:

```
```
tar -zxvf aide-<NNNN>.tar.gz
cd aide-<NNNN>
./configure
make
make install
```
```

# # Configuring AIDE

AIDE, like many other Linux applications, operates using a configuration file. The configuration file is text-based and contains information that the program uses to determine the characteristics it will use when it runs. The first time you run AIDE you'll create and initialize the database that will be used for future checks of the filesystem's integrity. That database is then manually checked over for sanity, and you'll run an update process that will be used from then on to look for changes that occur on the filesystem.