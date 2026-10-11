
In a single-package spec file, nothing explicitly identifies the preamble other than its position at the top of the file. For subpackages, however, we need to be a bit more explicit. So we use the `%package` directive to identify the preamble for each subpackage.

## 18.4.1.1. The `%package` Directive

The `%package` directive actually performs two functions. As mentioned, it is used to denote the start of a subpackage's preamble. It also plays a role in forming the subpackage's name. For example, let's say the main preamble contains the following `name` tag:

```
name: foo
```

Later in the spec file, there is a `%package` directive:

```
%package bar
```

This would result in the name of the subpackage being foo-bar.

In this way, it's easy to see the relationship of the subpackage to the main package (or to other subpackages, for that matter). Of course, this naming convention might not be appropriate in every case. So there is an option to the `%package` directive for just this circumstance.

## 18.4.1.2. Adding `-n` to the `%package` Directive

The `-n` option is used to change the final name of a subpackage from *mainpackage-subpackage* to *subpackage*. Let's modify the `%package` directive in our earlier example to be

```
%package -n bar
```

The result is that the subpackage name would be bar instead of foo-bar.

## 18.4.1.3. Updating Our Spec File

Let's apply some of our newly found knowledge to the spec file we're writing. Here's the list of subpackages we need to create:

- The server subpackage, to be called foo-server
- The client subpackage, to be called foo-client
- The baz development library subpackage, to be called bazlib

Since our package name is foo, and since the `%package` directive creates subpackage names by prepending the package name, the `%package` directives for the foo-server and foo-client subpackages would be written as

```
%package server
```

and

```
%package client
```

Since the baz library's package name is not to start with foo, we need to use the -n option on its %package directive:

```
%package -n bazlib
```

Our requirements further state that foo-server and foo-client are to have the same version as the main package.

One of the time-saving aspects of using subpackages is that there is no need to duplicate information for each subpackage if it is already defined in the main package. Therefore, since the main package's preamble has a version tag defining the version as 2.7, the two subpackages that lack a version tag in their preambles will simply inherit the main package's version definition.

Since the bazlib subpackage's preamble contains a version tag, it must have its own unique version.

In addition, each subpackage must have its own summary tag.

So, based on these requirements, our spec file now looks like this:

```
Name: foo
Version: 2.7
Release: 1
Source: foo-2.7.tgz
CopyRight: probably not
Summary: The foo app, and the baz library needed to build it
Group: bogus/junk
%description
This is the long description of the foo app, and the baz library needed to build it...

%package server
Summary: The foo server

%package client
Summary: The foo client

%package -n bazlib
Version: 5.6
Summary: The baz library
```

We can see the subpackage structure starting to appear now.

## 18.4.1.4. Required Tags in Subpackages

There are a few more tags we should add to the subpackages in our sample spec file. In fact, if these tags are not present, RPM will issue a most impressive warning:

```
# rpm -ba foo-2.7.spec
Package: foo-server
Field must be present: Description
Field must be present: Group

Package: foo-client
Field must be present: Description
Field must be present: Group
Package: bazlib
Field must be present: Description
Field must be present: Group

Spec file check failed!!
Tell rpm-list@redhat.com if this is incorrect.
```

Our spec file is incomplete. The bottom line is that each subpackage *must* have these three tags:

- The `description` tag
- The `group` tag
- The `summary` tag

It’s easy to see that the first two tags are required, but what about summary? Well, we lucked out on that one: We already included a *summary* for each subpackage in our sample spec file.
Let’s take a look at the `description` tag first.

### 18.4.1.5. The `description` Tag

As you’ve probably noticed, the `description` tag differs from other tags. First of all, it starts with a percent sign, making it look similar to a directive. Second, its data can span multiple lines. The third difference is that the `description` tag must include the name of the subpackage it describes. This is done by appending the subpackage name to the `description` tag itself. So, given these `package` directives:

```
%package server
%package client
%package -n bazlib
```

our `description` tags would start with

```
%description server
%description client
%description -n bazlib
```

Notice that we’ve included the `-n` option in the `description` tag for `bazlib`. This was intentional, as it makes the name completely unambiguous.

### 18.4.1.6. Our Spec File So Far

Okay, let’s take a look at the spec file after we’ve added the appropriate `descriptions`, along with group tags for each subpackage:

```
Name: foo
Version: 2.7
Release: 1
Source: foo-2.7.tgz
CopyRight: probably not
Summary: The foo app, and the baz library needed to build it
Group: bogus/junk
%description
This is the long description for the foo app, and the baz library needed to build it...

%package server
Summary: The foo server
Group: bogus/junk
%description server
This is the long description for the foo server...

%package client
Summary: The foo client
Group: bogus/junk
%description client
This is the long description for the foo client...

%package -n bazlib
Version: 5.6
Summary: The baz library
Group: bogus/junk
%description -n bazlib
This is the long description for the bazlib...
```

Let's take a look at what we've done. We've created a main preamble as we normally would. We then created three additional preambles, each starting with a %package directive. Finally, we added a few tags to the subpackage preambles.

But what about version tags? Aren't the server and client subpackages missing them?

Not really. Remember that if a subpackage is missing a given tag, it will inherit the value of that tag from the main preamble. We're well on our way to having a complete spec file, but we aren't quite there yet.

Let's continue by looking at the next part of the spec file that changes when building subpackages.

## 18.4.2. The %files List

In an ordinary single-package spec file, the %files list is used to determine which files are actually going to be packaged. It is no different when building subpackages. What is different is that there must be a %files list for each subpackage.

Since each %files list must be associated with a particular %package directive, we simply label each %files list with the name of the subpackage, as specified by each %package directive. Going back to our example, our %package lines were

```
%package server
%package client
%package -n bazlib
```

Therefore, our `%files` lists should start with

```
%files server
%files client
%files -n bazlib
```

In addition, we need the main package’s `%files` list, which remains unnamed:

```
%files
```

The contents of each `%files` list is dictated entirely by the software’s requirements. If, for example, a certain file needs to be packaged in more than one package, it’s perfectly all right to include the filename in more than one list.

### 18.4.2.1. Controlling Packages with the `%files` List

The `%files` list wields considerable power over subpackages. It’s even possible to prevent a package from being created by using the `%files` list. But is there a reason you’d want to go to the trouble of setting up subpackages, only to keep one from being created?

Actually, there is. Take, for example, the case where client/server-based software is to be packaged. Certainly, it makes sense to create two subpackages: one for the client and one for the server. But what about the main package? Is there any need for *it*?

Quite often there’s no need for a main package. In those cases, removing the main `%files` list entirely will result in no main package being built.

### 18.4.2.2. A Point Worth Noting

Keep in mind that an empty `%files` list (that is, a `%files` list that contains no files) is *not* the same as not having a `%files` list at all. As noted previously, entirely removing a `%files` list results in RPM not creating that package. However, if RPM comes across a `%files` list with no files, it will happily create an empty package file.

This feature (which also works with subpackage `%files` lists) comes in handy when used in concert with conditionals. If a `%files` list is enclosed by a conditional, the package will be created (or not) based on the evaluation of the conditional.

### 18.4.2.3. Our Spec File So Far

Okay, let’s update our sample spec file. Here’s what it looks like after adding each of the subpackages’ `%files` lists:

```
Name: foo
Version: 2.7
Release: 1
Source: foo-2.7.tgz
CopyRight: probably not
```
