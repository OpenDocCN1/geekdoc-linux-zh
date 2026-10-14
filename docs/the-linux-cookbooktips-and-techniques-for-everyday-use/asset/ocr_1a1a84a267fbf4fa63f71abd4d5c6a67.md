# 16.4 Typesetting with TeX and Friends

```
@sf(Debian): `tetex-base`
@sf(Debian): `tetex-bin`
@sf(Debian): `tetex-doc`
@sf(Debian): `tetex-extra`
@sf(Debian): `tetex-lib`
@sf(WWW): http://www.tug.org/teTeX/
```

The most capable typesetting tool for use on Linux-based systems is the TeX typesetting system and related software. It is the premier computer typesetting system—its output surpasses or rivals all other systems to date. The advanced line and paragraph breaking, hyphenation, kerning, and other font characteristic policies and algorithms it can perform, and the level of precision at which it can do them, have yet to be matched in word processors.

The TeX system itself—not a word processor or single program, but a large collection of files and data—is packaged in distributions; teTeX is the TeX distribution designed for Linux.

TeX input documents are plain text files written in the TeX formatting language, which the TeX tools can process and write to output files for printing or viewing. This approach has great benefits for the writer: the plain text input files can be written with and exchanged between many different computer systems regardless of operating system or editing software, and these input files do not become obsolete or unusable with new versions of the TeX software.

Donald Knuth, the world's foremost authority on algorithms, wrote TeX in 1984 as a way to typeset his books, because he wasn't satisfied with the quality of available systems. Since its first release, many extensions to the TeX formatting language have been made—the most notable being Leslie Lamport's LaTeX, which is a collection of sophisticated macros written in the TeX formatting language, designed to facilitate the typesetting of structured documents. (LaTeX probably gets more day-to-day use than the plain TeX format, but in my experience, both systems are useful for different kinds of documents.)

The collective family of TeX and related programs are sometimes called "TeX and friends," and abbreviated as `texmf` in some TeX references(26); for example, the supplementary files included with the bare TeX system are kept in the `/usr/lib/texmf` directory tree.

The following recipes describe how to begin writing input for TeX and how to process these files for viewing and printing. While not everyone wants or even has a need to write documents with TeX and LaTeX, these formats are widely used—especially on Linux systems—so every Linux user has the potential to encounter one of these files, and ought to know how to process them.

NOTE: "TeX" doesn't sound like the name of a cowboy, nor "LaTeX" like a kind of paint: the letters `T`, `E`, and `X` represent the Greek characters tau, epsilon, and chi (from the Greek `techne`, meaning art and science). So the last sound in "TeX" is like the `ch` in `Bach`, and "LaTeX," depending on local dialect, is pronounced either `lay-teck` or `lah-teck`. Those who become highly adept at using the system, Knuth calls "TeXnicians."