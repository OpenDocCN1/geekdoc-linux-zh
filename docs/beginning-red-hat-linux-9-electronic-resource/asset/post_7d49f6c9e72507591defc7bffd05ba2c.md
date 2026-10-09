
![](img/b852150740856958b10aff9e8c9d2adc_168_0.png)

There are two options for each of the three office applications that support VBA code embedding. These options are:

| Option | Description |
|---|---|
| Load Basic code to edit | When this option is selected, the application will load the VBA code from the original document and embed it into a special Basic module within OpenOffice. This module will preserve the code and allow you to edit it through the application’s interface or IDE. |
| Save Original Basic Code again | When this option is selected, the application will save the code as preserved in the Basic module in the format expected of the Office application, so the code will continue to work as expected (assuming its syntax is correct). |

> It is beyond the scope of this chapter to cover BASIC within OpenOffice. If you want to know more, take a look at http://www.engineering.usu.edu/cee/faculty/gurro/Software_Calculators/StarOffice_Docs/StarOfficeBasicManual.zip. StarOffice Basic is very similar to OpenOffice Basic, and you can switch between OpenOffice and VBA Help (if you run Windows) to find assistance.

## Microsoft Office Options

Microsoft Office’s applications also allow users to embed objects of one type within another. For example, if you wanted to show some sales data from a spreadsheet within your sales report, then you can easily embed your Excel spreadsheet within your Word document. In Microsoft parlance, this is known as Object Linking and Embedding (or OLE). With OLE, the embedded object inherits the functionality of the application it was created in (so in the example cited here, the embedded Excel spreadsheet inherits the functionality of MS Excel, even though it is embedded into an MS Word file).

The Options dialog box in OpenOffice allows us to select which objects are converted (if at all) and at which stage – either when the object is loaded into OpenOffice and/or saving from OpenOffice into a Microsoft format:

![](img/b852150740856958b10aff9e8c9d2adc_169_0.png)

The checkboxes in the [L] (for "load") column indicate that an object of the specified type should be converted into an OpenOffice object when a Microsoft document is loaded. The checkboxes in the [S] (for "save") column indicate that the object should be converted to the specified Microsoft Object when the document is saved to a Microsoft file format. (So, if you leave the [S] checkbox unchecked, the objects will *not* be converted and will be absent from the resulting file.)

As you can see from the screenshot above, there are four object types supported, including Microsoft Word (WinWord), Microsoft Excel, Microsoft PowerPoint, and MathType.

*MathType is an application used for representing mathematical formulae. For more on this application, see http://www.mathtype.com/mathtype.*

## HTML Compatibility Options

This dialog doesn't offer any features for converting between versions of Microsoft Office, but it does contain the setting that indicates what browser is targeted when exporting a document from an OpenOffice application in **HTML format**. OpenOffice supports a number of formats, including:

- Netscape Navigator (version 3.0 and 4.0)
- Microsoft Internet Explorer (version 4.0)
- HTML 3.2 (most browsers support this)

![](img/b852150740856958b10aff9e8c9d2adc_170_0.png)

## File Format Options

In addition to the settings within the **Options** dialog, OpenOffice's ability to load from (and save to) different file formats is integral to the applications themselves. These options vary according to the context of the application, and so they are covered within the OpenOffice applications themselves.

However, it's also worth noting the existence of a generic document conversion tool called **AutoPilot**, which is accessible from all OpenOffice applications. If you select File | AutoPilot | Document Converter, you'll see a dialog box like the one shown below:

![](img/b852150740856958b10aff9e8c9d2adc_171_0.png)

*AutoPilot* is actually a batch tool, for which OpenOffice provides a shortcut.

This dialog provides you with options to convert from StarOffice or Microsoft Office file formats to the new OpenOffice XML (eXtended Markup Language) format. In the screenshot above, we're concentrating on Microsoft Office file formats and a Word document we have to convert, so we've marked the Word documents option.

After pressing Next, you'll see the dialog box shown below. It prompts us to say whether we wish to convert templates, documents, or both, and whether we are to include sub-directories in our conversion process. In this case, we're converting only Word documents from our working directory and placing the converted files in the same directory:

![](img/b852150740856958b10aff9e8c9d2adc_172_0.png)

When you click the Next button again, you'll see a confirmation dialog box. If you're happy that everything is present and correct, select the Convert button and the conversion process will begin:

![](img/b852150740856958b10aff9e8c9d2adc_172_1.png)

When the conversion is complete, the Progress screen will display the results of the conversion process.

Note that this conversion process will render any VBA code invalid. If your documents contain VBA code that you wish to preserve, you should avoid this method.

### Conversion Quality and Considerations

It’s worth mentioning that the conversion quality between different file formats (especially Microsoft Office) is excellent. The only caveats are that the conversion process from OpenOffice to Microsoft Office can lead to files larger that their original file sizes due to the lack of compression. However, this is likely to change in future releases.

It’s worth experimenting with the Rich Text Format or RTF file format – this will help to avoid potential conversion errors, although at the expense of certain formatting capabilities. Another option is to link your graphics to external files instead of embedding them within your documents.

### Using OpenWriter for Word Processing

When you start OpenOffice’s **OpenWriter** (or just **Writer**) word processing application (which you can do using **Main Menu | Office | OpenOffice.org Writer** or the shortcut icon from the task bar), you are presented with a window like the one below:

![](img/b852150740856958b10aff9e8c9d2adc_173_0.png)

OpenWriter provides the wealth of features that one would normally expect to find in a commercial word processing application. We won't list them all here; like the other applications in the suite, it would warrant a book in its own right. However, we will highlight some of the key features included and also describe how interoperability with other applications such as Microsoft Office is achieved. Some of the key features present are:

- Styles and style galleries
- Thesaurus
- Spell checker
- Clipart
- Support for other file formats, such as Microsoft Word, StarWriter, and so on

As we've seen, OpenWriter is compatible with Microsoft Word. In particular, it is capable of loading and saving documents and templates in a number of Word file formats, including Microsoft Word 97/2000/XP and Microsoft Word 6.0/95. You can load and save between OpenOffice's native version and any of the other versions listed, simply by using the File | Open and File | Save dialogs. The File Type drop-down box allows you to choose the appropriate format:

![](img/b852150740856958b10aff9e8c9d2adc_174_0.png)

### Using OpenCalc for Spreadsheets

OpenOffice's **OpenCalc** (or *Calc*) application again provides numerous features that you would expect of a commercial application and is comparable with Microsoft Excel, the spreadsheet application within Microsoft Office. Some of the key features present are:

- Ability to handle multiple spreadsheets simultaneously
- Embedded graphics and charts
- Cell security
- External data sources
- Data Pilot (this is similar to PivotTables in Excel)

OpenCalc also supports compatibility with Excel, in its ability to load and save spreadsheets and templates in a number of Excel file formats, including Microsoft Excel 97/2000/XP and Microsoft Excel 4.x–5.0. Other interoperability features include the handling of VBA code and embedded objects (as we mentioned earlier in this chapter).

There are other, more specific options that mimic the behavior of MS Excel, and help to make users with an MS Excel background feel more comfortable. One specific such option is the ability to indicate that OpenCalc's searching capability should behave in the same manner as Excel's. This option can be found in the Tools | Options dialog box, in the Spreadsheet | Calculate tab:

![](img/b852150740856958b10aff9e8c9d2adc_175_0.png)

Note the Search criteria = and <> must apply to whole cells option in this dialog. When this option is selected, OpenCalc handles searches in the same way as Microsoft Excel, in that the search criteria entered are specific and must match the whole cell. When the option is unselected, the search criteria are matched against *any* position within the cell.
