
## IN-DEPTH

### Programming Snapshot – Rotating Photos with Go

#### Listing 5: autorot.go

```go
package main

import (
    "flag"
    "fmt"
    "github.com/twcarns1n/goexif/exif"
    "os"
    "path"
)

func main() {
    flag.Usage = func() {
        fmt.Printf("Usage: %s jpg-file\n", path.Base(os.Args[0]))
        os.Exit(1)
    }

    flag.Parse()
    if len(flag.Args()) != 1 {
        flag.Usage()
    }

    jpgFile := flag.Arg(0)

    f, err := os.Open(jpgFile)
    if err != nil {
        panic(err)
    }

    data, err := exif.Decode(f)
    if err != nil {
        panic(err)
    }

    orient, err := data.Get(exif.Orientation)
    if err != nil {
        fmt.Printf("No orientation header found.\n")
        os.Exit(0)
    }

    val, err := orient.Int(0)
    if err != nil {
        panic(err)
    }

    switch val {
    case 3:
        imgMod(jpgFile, jpgFile, rot180)
    case 6:
        imgMod(jpgFile, jpgFile, rot90)
    default:
        panic("Unknown orientation")
    }
}
```

Use `imgMod` with the appropriate algorithm function as a parameter. The calls to `imgMod()` in Listing 5 use identical names for the source and target files so `autorot` simply overwrites the original files. If that seems too dangerous, you can rename the target file to `.bak`, and you’re guaranteed no accidents.

When Go’s image library writes the JPEG image back to disk, it completely omits the original Exif data, so there’s no longer an `orient` entry in the header there, indicating correct rotation.

#### Compiling the Program

You can use the command sequence from Listing 6 to create the `autorot` binary. The `go` compiler fetches the required libraries from GitHub, compiles them, and links them. As always, this creates an executable that already contains all the dependencies. It can be copied to another computer without any problems and will run there without any complaints, given a similar operating system and processor architecture.

#### Listing 6: Compiling autorot

```bash
$ go mod init autorot
$ go mod tidy
$ go build autorot.go rotate-90.go rotate-180.go imgmod.go
```

![](img/8286bf901ba268fe114d66ada92d1dd6_55_0.png)

#### Conclusions

The program is by no means perfect yet. It’ll work for most cases, but still lacks counterclockwise rotation and algorithms for more exotic Exif values. But with the described basics, these features can easily be added. As always, Go imposes no limits on the hobbyist here.

**Info**

1. Listings for this article: [http://ftp.linux-magazine.com/pub/listings/linux-magazine.com/257](http://ftp.linux-magazine.com/pub/listings/linux-magazine.com/257)
2. “Manipulating Stored Geocoordinates in Cellphone Photos” by Mike Schilli, Linux Magazine, issue 240, December 2020, [https://linux-magazine.com/issues/2020/240/Obfuscation-Filter](https://linux-magazine.com/issues/2020/240/Obfuscation-Filter)

---

![](img/8286bf901ba268fe114d66ada92d1dd6_56_0.png)

![](img/8286bf901ba268fe114d66ada92d1dd6_56_1.png)

**LINUX MAGAZINE**
20 YEAR ARCHIVE DVD

ORDER NOW!
[https://bit.ly/Archive-DVD](https://bit.ly/Archive-DVD)

![](img/8286bf901ba268fe114d66ada92d1dd6_56_2.png)

---

## IN-DEPTH

### LibreOffice vs OpenOffice

![](img/8286bf901ba268fe114d66ada92d1dd6_57_0.png)

#### Comparing LibreOffice and OpenOffice

**The Clear Choice**

While LibreOffice and OpenOffice have a shared past, LibreOffice outstrips OpenOffice in contributors, code commits, and features. By Bruce Byfield

A search for comparisons of LibreOffice and Apache OpenOffice returns over 8.3 million results. That number comes as no surprise, given that LibreOffice and OpenOffice are the best-known open source office suites and share a common past. However, what is surprising is how shallow many of the comparisons are. Many offer only a superficial glimpse at either office suite from the viewpoint of an unsophisticated and demanding user. Often, the comparisons are obsolete. Also important to note is that many comparisons strive for a false sense of objectivity by declaring that any differences are minor. However, by every possible standard, LibreOffice outshines OpenOffice and shows OpenOffice to be outdated. To pretend otherwise is a distortion of the truth.

As you might know, the two office suites share a common history (Figure 1). Both originate in OpenOffice.org, a project run by Sun Microsystems from 2000-2011. In fact, OpenOffice claims to be the legal descendent of OpenOffice.org because in 2011 Sun passed OpenOffice.org to Oracle, which in turn passed it on to the Apache Foundation – but the concept of ownership has little relevance in open source. At the same time, Go-o.o, a semi-official fork that had operated quietly since 2007, created LibreOffice and its governing body, The Document Foundation. Go-o.o had been contentious in OpenOffice.org because it advocated a faster pace of development, so the creation of the two new projects seemed to formalize a division that already existed.

Certainly LibreOffice and OpenOffice showed little love for one another from the beginning. Also from the start, OpenOffice faced challenges that LibreOffice did not. To start with, OpenOffice uses the Apache License, while LibreOffice uses a dual LGPLv3/Mozilla Public License (MPL). A major consequence of this difference in licenses is that LibreOffice can borrow code from OpenOffice, while OpenOffice cannot borrow code from LibreOffice. Just as importantly, from late March 2014 to March 2015, OpenOffice had a total of 16 contributors, 12 of whom stopped contributing when IBM stopped supporting OpenOffice [1]. Since then, OpenOffice has been reluctant to publish the number of contributors, but, considering that OpenOffice claimed 120 contributors in 2012 [2], it is doubtful that the number today is more than a small fraction of LibreOffice’s 1,722 [3]. The result is predictable: OpenOffice has not had a major release since 2014 and only 11 minor ones. In comparison, LibreOffice has had 13 major releases and 87 minor releases. And in 2019, LibreOffice had over 15,000 code commits and OpenOffice had 595 [4].

Equally inevitably, LibreOffice has attracted important corporate supporters such as Red Hat and Collabora while OpenOffice has been unable to fill the void left by IBM eight years ago. OpenOffice’s continued existence has been quaint, even admirable, but the project is simply not structured to compete.

**The Feature Disparity**

Aside from Go-o.o’s contributions a decade ago, the two projects initially

![](img/8286bf901ba268fe114d66ada92d1dd6_58_0.png)

shared a common codebase. Even today, enough code remains the same that extensions that run with one often run with the other's releases, although less often than a decade ago. No doubt the mutual use of Open Document Format (ODF) for files contributes to continued compatibility. However, the differences do seem to be growing — mostly due to LibreOffice's innovations. The difference can be seen in the download sizes: LibreOffice's DEB download file is 195MB, while OpenOffice's is 159MB. In other words, LibreOffice is close to one quarter larger, despite the fact that it has removed redundancies in the code and rewritten parts for greater efficiency; operations that OpenOffice has yet to duplicate.

About eight years ago, I saw a copy of a LibreOffice internal document that listed all the OpenOffice features that OpenOffice lacked. To my surprise, there were hundreds of line items. Even though many were minor, the differences are far too numerous to list, let alone to explain each one. However, among the more significant features, LibreOffice included an extensive overhaul of the interface, rearranging menu items, repositioning items in windows to make them more accessible, adding themes, and in general creating a more user-friendly look. These changes are especially noticeable in the Charts subsystem for spreadsheets, where the colors were updated from OpenOffice.org's stuck-in-the-1990s look. In addition, LibreOffice introduced themes and a choice of user interfaces that includes an MS Office-like ribbon toolbar. None of these changes have any equivalent in OpenOffice.

LibreOffice's new features are visible in all the modules, especially Writer and Calc. But in the interests of space, I will let Writer stand as an illustration of the others. Outstanding features in LibreOffice Writer that have no counterpart in OpenOffice are:

- The folding of Table Design into the other styles, where it is easy to find and can be copied over into other files.
- Default list styles with choices of bullet and numbering systems, saving users the need to set them up.
- Export to EPUB format (this feature is still being fully implemented, although it is often usable now).
- Support for HarfBuzz, a font-rendering app that allows the modification of OpenType and True Type files through a series of codes added in character fields, making LibreOffice a full-fledged desktop publisher.

However, for many users, the most important improvements in LibreOffice Writer are the continued enhancements for exporting to MS Word. This effort can be a moving target because Microsoft often alters its formats, but reliable import filters to MS Word are essential to many companies' adoption of LibreOffice. Much of this work is due to LibreOffice's strategic alliance with Collabora, which builds compatibility solutions for its customers and donates its improvements to LibreOffice, contributing over a third of LibreOffice's commits in 2019. In the recent 7.3 releases, the MS Word import and export filters are at a stage where most routine business and academic documents can be reliably exchanged with those not using LibreOffice. By contrast, OpenOffice's MS Word compatibility is much more erratic.

**The Latest Releases**

For still another perspective, you have only to look at the latest release notes. On November 27, 2021, OpenOffice announced the release of OpenOffice 4.1.11 [5]. The complete list of improved or enhanced features for this release is:

- Enabled persistent adjustment to help text font size.
- Added Fontwork to Insert menu.
- Added missing PDF export icon to File menu.

In addition, two bugs fixes were thought worthy of mention:

- New security warning introduced with Apache OpenOffice 4.1.10 blocks useful functions.
- The Windows installation file has missing properties and lacks a code signature.
- Windows installation: Lost adapted texts after switch to NIS 3.x.
- Chart lost when saving in ODS format.

Furthermore, no new or updated dictionaries or languages were added.

In comparison, the release notes for LibreOffice 7.3 [6], announced February 2, 2022, included so many new features and improvements that a complete list would be too long to include here.
