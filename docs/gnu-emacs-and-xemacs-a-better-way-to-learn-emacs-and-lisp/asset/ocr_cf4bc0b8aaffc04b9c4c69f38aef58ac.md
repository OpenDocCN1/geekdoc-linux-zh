A**SCII text is the Emacs native file format. ASCII (*American Standard Code for Information Interchange*) is a character encoding standard meant to be platform- and manufacturer-independent. Each character is represented by 7 bits (the smallest unit of storage for computers, equivalent to a binary digit). Here are some advantages of ASCII text:

+   - It is a worldwide standard that can be read by all software.
+   - It has minimal storage requirements.
+   - The files are relatively small.
+   - ASCII is not tied to the fate of any commercial entity.
+   - It’s versatile.
+   - It’s used for programmers’ source code, e-mail, and input to text processors.

The simplicity of ASCII text comes at a cost. No formatting information is built into the files beyond the breaking of lines that line feeds and/or carriage returns (these are invisible non-printing characters that make line-wrapped files possible). Font information is lacking; the appearance of such files depends on the capabilities of the video display or the printer’s built-in fonts. It is a bare-bones file format, but you can be sure that anything saved in plain text will be readable in the future, a guarantee that can’t be made by vendors of proprietary binary file formats.

![](bbox=[0.08, 0.62, 0.14, 0.72])

> A binary file cannot be read in a text editor. Executable or shared library files on your Linux system are binary files. Commercial applications such as word processors and spreadsheets have traditionally used binary file formats for a user’s documents. These file formats can be changed at the whim of the software vendor and often aren’t read accurately by other manufacturers’ products.

Although formatting information isn’t a part of a plain-text file, a variety of text-processing languages and systems can be used to add that formatting to an ASCII text file in the form of markup or tags, special characters that tell the text-processing system how to represent sections of text. This chapter introduces several methods of writing text with Emacs, processing the file, and ending up with a professional-looking printable file.

# Text Processing and Word Processing

Word processors have become ubiquitous in recent years. They provide an easy way to produce formatted documents, but they do have a few limitations. The