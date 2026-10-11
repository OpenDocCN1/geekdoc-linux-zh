# 13.7.1. `-n <string>`: Use `<string>` As the Entire Subpackage Name

As mentioned earlier, the name of a subpackage normally includes the main package name. When the `-n` option is added to the `%package` directive, it directs RPM to use the name specified on the `%package` line as the entire package name. In the preceding example, the following `%package` line would create a subpackage named `foon1y-doc`:

```
```
%package doc
```

```

The following `%package` line would create a subpackage named `doc`:

```
```
%package -n doc
```

```

The `%package` directive plays another role in subpackage building: to act as a place to collect tags that are specific to a given subpackage. Any tag placed after a `%package` directive will apply only to that subpackage.

Finally, the name string specified by the `%package` directive is also used to denote which parts of the spec file are a part of that subpackage. This is done by including the string (along with the `-n` option, if present on the `%package` line) on the starting line of the section that is to be subpackage specific. Here’s an example:

```
```
###
%package -n bar
###
%post -n bar
###
```

```

In this heavily edited spec file segment, a subpackage called `bar` has been defined. Later in the file is a postinstall script. Because it has subpackage `bar`’s name on the `%post` line, the postinstall script will be part of the `bar` subpackage only.

For more information on building subpackages, see Chapter 18, “Creating Subpackages.”

# 13.8. Conditionals

While the `exclude` and `exclusive` tags (`exclusivearch`, `exclusiveos`, `excludedos`, and `excludedos`) provide some control over whether a package will be built on a given architecture and/or operating system, that control is still rather coarse.

For example, what should be done if a package will build under multiple architectures, but requires slightly different `%build` scripts? Or what if a package requires a certain set of files under one operating system, and an entirely different set under another operating system? The architecture and operating system–specific tags discussed earlier in the chapter do nothing to help in such situations. What can be done?