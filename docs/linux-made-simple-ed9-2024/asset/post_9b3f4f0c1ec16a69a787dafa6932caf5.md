
## PDFs: Edit and annotate

Portable they may be, but accessible? Not without a little hard work and determination.

**Quick tip**

LiveOffice Draw is capable of editing PDFs, but it's not always tip top when it comes to saving them out. It's worth trying, if you have complex tasks to perform.

We’ve all seen PDFs, haven’t we? They’re neat little document packages which contain all the fonts and layout information required to display exactly what the creator intended, without requiring any of the software that was used to make them. They’re also, usually, incredibly small. Hence the name Portable Document Format: universally supported on just about any system, almost always displayed correctly, and – at least these days – outputtable to PDF just about any creative software.

But there’s a problem: PDFs tend to be one-way streets, documents designed to exist in a read-only state. Editing a PDF is not an easy task. But, as we’ll discover, there are ways around these restrictions: ways to get information out of PDFs, ways to tweak existing documents, and ways to create brand new PDFs from that source material.

## Money matters

First, let’s talk about the commercial options available to Linux users. There are two primary PDF editors on the market, PDF Studio and Master PDF Editor. The former comes in two flavours: Standard ($89), which can convert most documents to PDF, add annotations and comments to PDF documents, and split, merge or password protect your PDFs. For proper editing facilities you’ll have to plump for the Pro version ($129) which also adds batch processing facilities and optical character recognition to extract text from images. There are free trials available of both versions at qoppa.com. Slightly easier on the wallet at $36 is Master PDF Editor which, as its name implies, is pretty masterful at the task of editing PDF files, and also exporting them to various image formats, splitting and merging, document signing and much more. The reduced price, as far as we can tell, doesn’t mean a great loss of functionality. There’s a free evaluation version to download at code-industry.net so you can see if you like it before plunking down the cash.

![](img/420a7272a6efa239082a35eeadd9bc1d_51_0.png)

Gscan2pdf, using the Tesseract OCR engine, does a pretty decent job of extracting text from images but struggles with more complex fonts.

There are other ways to perform the main functions of proper PDF editors without shelling out a penny, but they’re all limited in their own way. So let’s look at a few of the tasks you might want to perform, and how to get them done.

## Optical Character Recognition

OCR, as it’s less tongue-twistingly known, is the process of getting words out of pictures. So if someone’s sent you a PDF of a scanned document, that’s exactly what you’re dealing with: a picture, just one in a nice package. In order to turn these printed characters back into editable text, your computer needs to, in base terms, trace over a bunch of pixels to work out what letters they might represent, then output that text.

We’d recommend a package called gscan2pdf for this task. It’s primarily meant for turning images into PDFs – hey, another task ticked off the list – but it also has an OCR export feature built in. Install it from your package manager, run it, and hit [Ctrl+H] to import your PDF. If it’s slightly off-kilter, you’ll first want to use Tools > Clean Up to automatically adjust the text to be on a straight line, otherwise the OCR engine might get a bit confused. Make sure you only have a single edge checkbox selected, otherwise the deskew function won’t work well. Click OK and your image should be adjusted.

Now let us run the actual OCR process. Go to Tools > OCR, and you’ll see Tesseract listed as the OCR engine. This is also available on the command line, and it’s a highly powerful tool, but rather difficult to run without some help – which is just what gscan2pdf is offering us. Check 'Threshold before OCR', and click 'Start OCR.' Click out Output tab, and you’ll see the results. Trickier fonts might not read perfectly, so you can click problem words to correct them here if you spot any issues. Hit [Ctrl+S] to save, and open up your PDF in the viewer of your choice – you can now select the text with your mouse and copy and paste to your heart’s desire.

## Image editing

If you're pulling images out of PDFs, or you want to change their design, there's really only one sensible free choice in the Linux domain: GIMP. That's not to say it's the only choice – there are plenty of image editors that can read PDFs – but GIMP is at the top of the heap. You likely already have it installed – it's in your package manager if not. Getting started with editing is just a case of opening the PDF using GIMP's Open command ([Ctrl]+[O]) and importing it as an image. You're then free to use GIMP's photo editing tools to manipulate it as if it were any other picture.

When you're finished, you'll need to use File > Export to save it out again as a PDF. This does have its downsides, though: GIMP's standard import procedure flattens the PDF out, so you'll lose any text layers you might have previously had.

## Annotation

When you need to take notes on a PDF, you could do a lot worse than using Xournal. Ostensibly a note-taking application, it's actually the perfect alternative to printing out your PDF, scribbling on it with a Sharpie, then scanning it back in again – with a couple of other key benefits.

Start by downloading Xournal from your distro's package manager, then run it. Go to File > Annotate PDF, open your PDF, and start scribbling away with the left mouse button. If it doesn't work – we've had this issue on some machines – try toggling Options > Use Xinput to off.

Xournal offers a few handy tools. The pen, the default tool, lets you draw – or scrawl – pen marks on top of your document. The eraser, which you can automatically switch to and use by holding the right mouse button, scrubs out marks you've previously made. The highlighter is pretty useful, in that it works like a regular highlighter pen, smearing a bright colour while letting the text below shine through. When you're using it, try clicking the checkered colour box on the right hand side of the toolbar to alter its colour, and drag the opacity slider to select how bold you want this effect to be.

Next up is the text tool: just click anywhere on the document and type in your text notes. You can tweak the font with the rightmost element of the toolbar, and change any text you've already written by double clicking it with the text tool selected. You can insert images as notes with the next icon, toggle the following icon to automatically turn your crude scrawls into geometric shapes, and force straight line drawing by activating the ruler icon.

When you're finished, just head to File > Export To PDF and save your work as a new PDF file. Again, you'll lose any additional layers (like raw text, which will be tricky to OCR with your scribbles on top), but you can pass on your annotated PDF to colleagues, victims, or even friends.

![](img/420a7272a6efa239082a35eeadd9bc1d_52_0.png)

![](img/420a7272a6efa239082a35eeadd9bc1d_52_1.png)

> **Quick tip**
> You can convert many common formats to PDF using free online tools: we recommend trying cloudconvert.com first of all.

## Inside Xournal

- **Zoom zoom**
  The magnifying glass is the only easy way to control your zoom level, particularly useful on high-resolution PDF files.

- **Drawing tools**
  Define your scribbles: will you use a pen? A highlighter? Infinitely neater text boxes? Pick your tools here and get annotating.

- **Move it around**
  The selection tools let you grab your scrawled notes and shift them around without affecting the background layer. Note that you'll need to.

- **Size it up**
  Xournal offers only a limited selection of tool sizes, so on high-res PDFs your notes may be a little small unless you use the biggest.

- **Colour theory**
  There are hotro's pre-defined and bold colours, perfect for highlighting, but click the rightmost icon to select an original colour of your own.

- **Face time**
  Use this button to select your text typeface – it won't affect notes you've already written, though.

![](img/420a7272a6efa239082a35eeadd9bc1d_52_2.png)
