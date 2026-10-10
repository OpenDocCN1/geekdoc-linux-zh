Save `local.conf`, and we are ready to build a cross-tool chain and a set of images. OE-Core provides a set of predefined targets that we can use to build our own images. A couple of these were listed by `oe-init-build-env`. To see the complete set of image targets execute:

```
ls .../meta/*-recipes*/images/* .bb
```

Now to build the `core-image-minimal` image, we simply execute:

```
bitbake core-image-minimal
```

# OE Metadata

While the image is “baking,” it is an opportunity to explore OE metadata. The `metadata` that drives BitBake consists of recipes and configuration files. Recipes get the file extension `*.bb`, and configuration files get the extension `.conf`. All of this metadata resides in the subdirectory `meta/`. Although it is not obvious from the layout of `meta/`, the recipes are divided into a hierarchy of four categories:

+   * Image
+   * Task
+   * Package
+   * Class

The motivation for the hierarchical organization is that recipes in lower levels can be easily reused.

Image is the top level of the hierarchy. An image recipe defines what goes into a specific root file system image. It lists the tasks that make up the image. Have a look at `meta/recipes-core/images/core-image-minial.bb`. It installs one task, `packagegroup-core-boot`, and possibly others defined in `CORE_IMAGE_EXTRA_INSTALL`. It also inherits a class called `core-image`. Class files get the extension `.bbclass`, and reside in `meta/classes/`.

Task recipes typically represent aggregations of packages. In fact, many of them are named `packagegroup-*`. For example take a look at `packagegroup-core-boot.bb`. It claims to be “The minimal set of packages required to boot the system.” Among other things, it inherits a class called `packagegroup`.

A package recipe manages the specific needs of an individual package. Package recipes typically have a version number appended to the name. `meta/recipes-core/sysvinit/sysvinit_2.88dsf.bb` is a typical example. It identifies where the package is found on the net, the license terms, the required files, and so on.