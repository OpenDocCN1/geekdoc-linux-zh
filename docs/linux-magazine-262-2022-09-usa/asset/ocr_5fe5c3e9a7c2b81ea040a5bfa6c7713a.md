![](bbox=[0.08, 0.08, 0.89, 0.32])

Figure 8: The Manuscript Outline panel shows the status of all chapters and makes it easy to rearrange them.

writing (maybe against your intentions, or what you believed to be your intentions).

# Configuration and Export Options

Most of what you see in Figures 3 to 10 is configurable by clicking on either View or *Edit / Settings* in Manuscript's top menu. You may, for example, add custom labels or writing statuses (Figure 12), as well as configure revision control or the theme of the full-screen editor.

As far as Manuscript's editor is concerned, it accepts and saves everything you write as plain text or as HTML, Markdown, or pretty much any other markup language (but please note that, at time of writing, the only format for which syntax highlighting is supported is *Markdown*). However, Manuscript can import existing texts in many formats, including but not limited to OpenDocument, .docx, ePub, and LaTeX.

On the output side, you can save or, as Manuscript confusingly calls it, 'compile' your finished work in all the formats supported by the Pandoc converter [6]. For both importing and exporting text, this is a mandatory prerequisite to make the most out of Manuscript.

Under the hood, every Manuscript writing project is composed of eight small files in text-based formats such as YAML, JSON, XML, or OPL, plus two folders. The eight files contain all the settings for that project, its labels and possible statuses, the summary, the plots, and so on. The two folders include one for the characters and one for the actual text that you write. Each character gets one file, which stores everything about the character formatted as key-value pairs. The beginning of Gandalf's file, for example, would look like Table 1.

The outline folder is divided into subfolders with the same structure that you see in Manuscript's *Outline* panel. Each of those subfolders contains a file called *folder.txt* that stores (with the same syntax used for characters) the metadata for that folder – that is, title, summary, expected word count, and so on. The single chapters, instead, are

![](bbox=[0.43, 0.67, 0.93, 0.95])

Figure 10: The actual Manuscript editor, supported by a panel listing all the properties of the current chapter and by a story line with all the plots and subplots.

![](bbox=[0.08, 0.77, 0.35, 0.94])

Figure 9: When you open the editor, the summaries of all chapters are visible as index cards.