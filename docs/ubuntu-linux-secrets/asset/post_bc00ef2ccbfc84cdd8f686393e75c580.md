
## Working with Math

If you have never used software like this, it helps to work through a simple example to see what is involved in creating a mathematical formula you can export to your Writer document.

Here’s a simple exercise you can do to get a feel for using Math:

- 1. Right-click in the Commands window. The main shortcut menu opens.
- 2. Select a submenu to open. We’ll select the Formats submenu for this exercise.
- 3. Select a formula component within this submenu. To follow along with this exercise, choose the matrix {...} entry. The template for the matrix code that’s needed in order to add a matrix to the formula appears in the Commands dialog box. It uses the <> symbol to indicate an entry in the matrix equation that you must replace. Also, the actual matrix layout appears in the main window. The combination is shown in Figure 7-12.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_222_0.png)

Figure 7-12: Starting to add a matrix in Math.

If you prefer to select the mathematical symbols visually rather than by their names, select the View Selection option from the menu bar. This produces the Selection dialog box with two sections. The top section contains buttons for each of the symbol categories. As you select a symbol category, the symbols contained in that category appear in the bottom section of the dialog box.

Just click on the symbol you want to use, and it appears in the command window.

## Part 2: Starting Out with Ubuntu

- 4. Replace each of the <?> entries with the proper letters and numbers for your formula.

When you change matrix[<?> # <?> # <?> # <?>] to matrix[A # B # C # D], Math automatically places the output in the main window.

- 5. Continue adding components to the formula until you’re finished.

Suppose that you want to multiply the matrix by 3. To find out the proper format for multiplication, press Enter to go down to the next line in the Commands window (to use as “scratch paper”), right-click to display the pop-up menu, and choose Unary/Binary Operators → A times b. This choice adds the phrase <?> times <?> beneath the matrix code. Now you know how to format a multiplication, so erase this phrase and use it as a guideline to change your formula to:

```text
3 times matrix{A # B ## C # D}
```

This line gives the result shown in Figure 7-13.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_223_0.png)

**Figure 7-13:** A complete formula in OpenOffice.org. Math.

Once you've created your formula you can save it using OpenDocument format (.odf), the StarOffice format (.sxm), and MathML 1.01 (.mml) format. The MathML format is a standard similar to HTML for working on the Web. You can also use the Export to PDF button in the standard toolbar to create a PDF document with your new formula.

## Summary

This chapter walked through the world of OpenOffice.org, the standard office productivity suite used in Ubuntu. OpenOffice.org provides several applications to help with your office automation needs. The Writer application provides word-processing capability and can be used to read and save documents in Microsoft Word format. Likewise, the Calc program is a spreadsheet application that can read and save documents in Microsoft Excel format.

The Impress application provides presentation graphics capabilities to Ubuntu. Although it can read PowerPoint files, it is currently has limited functionality, so you might be restricted in what you can do. The Draw application provides additional graphical capabilities that allow you to create and manipulate image files using many common image formats.

The Base application provides personal database services. You can create tables, queries, forms, and reports in a graphical environment, using a local database file or by connecting to a remote network database server.

Finally, the chapter walked through the Math application. Math allows you to create complex mathematical formulas to insert into your Writer documents.

In the next chapter we’ll dive into the world of Internet software. These days, just about everyone uses the Internet, so having software to interact on the Internet is a must. Ubuntu provides several Internet applications by default, plus it provides some extended applications that are easy to install. We’ll walk through the most popular ones for various Internet functions.
