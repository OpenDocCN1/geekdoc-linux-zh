# *Performing page layout*

In Writer, page styles control the page layout, and each page can have its own style. The usual approach is to define three page styles: First Page, Left Page, and Right Page. Define the First Page with whatever applies to the first page, such as a special header and no page number. The Left Page is the style for the even numbered pages and the Right Page style is for odd numbered pages. For each page style, you can also define the page style that applies to the following page. The idea is to define Left Page as the next page style for First Page and Right Page as the style of the page that follows the Left Page style. That way, the page styles are correct for all the pages as long as you start with the First Page style. You may also want to define a Landscape page style so you can use it for pages that have to be in landscape orientation.

![](bbox=[0.13, 0.37, 0.22, 0.44])

If you are familiar with Microsoft Word, you know that the page setup — paper size, orientation, margins, and so on — applies to all pages in the document. In Writer, a page style does not automatically apply to the entire document. Instead, each page has its own page style. Of course, you can choose to apply the same page style to all the pages. Essentially, you have more fine-grained control over page layouts in Writer.

A typical page layout task is to insert objects created in other OpenOffice.org applications, such as a Calc spreadsheet, an Impress slide, or a Draw drawing. You can insert such objects by choosing **Insert\: Object\: OLE Object**. Incidentally, OLE stands for *Object Linking and Embedding*, which is just a fancy term for the ability to create a document by adding components, such as charts and drawings, that are created in different applications.

![](bbox=[0.13, 0.6, 0.22, 0.67])

When you add components, keep this caveat in mind: You can edit a component directly in the document only by using the application that originally created the component.

A component that you can insert into a Writer document is a mathematical formula, and I mean serious formulas with integral signs and Greek letters, such as alpha and sigma. If you're writing a scientific paper with complex equations, you'll really appreciate this feature of OpenOffice.org. Here's a typical sequence of steps to insert a formula into a Writer document (this process is similar for inserting other components):

+   1. Position the cursor and select **Insert\: Object\: Formula**.

The user interface changes to that of OpenOffice.org Math — an application for writing mathematical formulas and a small frame for the formula appears in the document. The formula is typed in that frame.

+   2. Select a formula type from the top two rows of the Selection window.

The lower rows in the Selection window show available formulas of that type. For example, the summation category (denoted by an uppercase Greek letter sigma) includes integral signs.