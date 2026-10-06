# 552 Part IV ♦ Running Applications

Other Microsoft Office applications offer similar functionality. PowerPoint can convert presentations to HTML and general image formats such as JPEG and TIFF. Excel can save tab- and comma-delimited files that are easily importable into a large number of applications.

If you make use of Access to save data, you may want to move data stored in Access's .mdb format to use a SQL database. SQL is more scalable, powerful, and virtually platform-independent. Migrating to SQL will preserve your data, but if your .mdb file will not open in OpenOffice.org, you will need to re-create any forms for accessing the data that you would like to continue.

If you are likely to receive Microsoft Office files and you are concerned about interoperability, here are some options to consider:

+   * Keep a copy of Microsoft Office installed using WINE and the CodeWeavers CrossOver Office plugin. For more information about CrossOver Office, visit CodeWeavers' site at www.codeweavers.com.

+   * Ask individuals sending you to use a less vendor-specific format, such as Adobe PDF. Document formatting can be exquisitely preserved and will be viewable by anyone capable of installing a PDF viewer, which supports virtually every operating system in use today.

+   * For forms that have user-editable fields, scripting, or complex embedded information, use HTML documents. Instead a compliant web browser will be able to interact with the document, and Microsoft Office applications universally support saving files into this.

![](bbox=[0.13, 0.565, 0.19, 0.595])

Before making any wholesale conversion from Microsoft Office, make sure the files you need to use will work as expected with the new office you have selected or that you can construct suitable replacements if needed. Testing ahead of time enables you to make necessary adjustments without having to endure the frustration of finding some document inaccessible or unusable.

# Using Traditional Linux Publishing Tools

With old-school text processors such as Groff and Tex, you can ignore document while writing. Plain-text macros postprocessors handle how to lay out a document for printing after writing is done. With word processors such as OpenOffice.org Word and StarOffice Writer, you may mark up text and see the basic layout of the document as you write.

Some attributes of the traditional Linux document preparation tools make them particularly suited for certain types of projects. TeX and Groff (which is based