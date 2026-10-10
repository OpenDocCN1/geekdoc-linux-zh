
## Tell Us What You Think!

As the reader of this book, *you* are our most important critic and commentator. We value your opinion and want to know what we’re doing right, what we could do better, what areas you’d like to see us publish in, and any other words of wisdom you’re willing to pass our way.

As an associate publisher for Sams, I welcome your comments. You can e-mail or write me directly to let me know what you did or didn’t like about this book—as well as what we can do to make our books stronger.

> *Please note that I cannot help you with technical problems related to the topic of this book, and that because of the high volume of mail I receive, I might not be able to reply to every message.*

When you write, please be sure to include this book’s title and author as well as your name and phone or fax number. I will carefully review your comments and share them with the author and editors who worked on the book.

- E-mail: `feedback@samspublishing.com`
- Mail: Sams Publishing
  800 East 96th Street
  Indianapolis, IN 46240 USA

## Introduction

This book is about database programming in Delphi 6 and Kylix. Most of the code in the book (with the exception of the dbExpress chapters) should also work with Delphi 5, but I have made no effort to test it.

### Who This Book Is For

This book targets Delphi 6 and Kylix database programmers. I assume that you already have an understanding of the Object Pascal language and that you know how to create a Delphi or Kylix application, drop components on a form, create and connect event handlers, and perform the various and sundry tasks required to produce a working application.

I further assume that you have some basic knowledge of databases and their terminology. For that reason, I won’t explain what table, view, column, and other database-related terms mean in this book.

This book also uses some of the standard components in its sample applications. Apart from data-aware components, I don’t explain how to use the standard components used in these samples, such as action lists, buttons, list boxes, and the like. If you need additional information on those components, please refer to the Delphi or Kylix help or to a general-purpose, third-party Delphi book.

### How This Book Is Organized

If you are new to Delphi/Kylix database programming, it is best to read the chapters in order. If you have some experience in database programming, and you want to learn only about dbExpress (for example), you can jump directly to the appropriate chapter(s) and read those. Whether you read sequentially or not, the following is a quick overview of what you’ll find in each of the chapters.

- Chapter 1, “Establishing and Using Database Connections,” introduces dbExpress, the new data-access technology provided with Delphi 6 and Kylix. It shows you how to connect to a database using dbExpress.
- Chapter 2, “dbExpress Datasets,” continues with the dbExpress overview and discusses the dataset components specific to dbExpress.
- Chapter 3, “Client Dataset Basics,” introduces client datasets and the TClientDataSet component, which provides for high-speed, in-memory datasets.
- Chapter 4, “Advanced Client Dataset Operations,” continues with the discussion of client datasets and goes into detail about a number of more advanced client dataset operations.
- Chapter 5, “Data-Aware Components,” introduces data-aware components, which provide a bridge between the data and user interface of an application, automatically displaying information from a dataset and allowing the user to enter new data.
- Chapter 6, “Data-Aware Grids,” continues with the data-aware component discussion to show you how to display and edit data in a grid format.
- Chapter 7, “Dataset Providers,” provides the foundation for multi-tier database development by introducing the concept of a provider.
- Chapter 8, “DataSnap,” shows how to create a true multi-tier database application by creating separate client and server applications that connect over a network.
- Chapter 9, “The ConMan Application,” develops a simple contact manager to illustrate multi-tier database development techniques in a real-world (albeit simplistic) application.

### VCL or CLX?

Because the technology discussed in this book applies equally well to Delphi 6 and Kylix (with the exception of Chapter 8, “DataSnap”), all the code listings in this book are CLX listings. The downloadable source code is provided in both CLX and VCL form, so if you don’t write cross-platform applications, you may want to experiment with the VCL code instead.

In case you aren’t familiar with these terms, VCL stands for Visual Component Library; it is the original, Windows-specific class library supported by Delphi. CLX stands for Component Library Cross-Platform (the X stands for Cross-Platform) and is the new, cross-platform class library supported both by Delphi and Kylix.

CLX is broken down into four categories:

- BaseCLX: This includes the “behind-the-scenes” utility classes and functions, such as TStringList, TObjectList, and so on.
- DataCLX: This wraps the CLX database functionality, such as dbExpress and data-aware components.
- VisualCLX: This includes visual components such as menu bars, toolbars, buttons, list boxes, and so on.
- NetCLX: This includes Internet-related components.

The only part of CLX specifically discussed in this book is DataCLX (although bits and pieces of BaseCLX and VisualCLX are used to create the sample CLX applications).

You’ll see from the code listings that apart from the uses clause at the top of each unit, there is almost no difference between the VCL code and CLX code, so you shouldn’t have any trouble following along with the CLX code.

To avoid clumsy constructs such as “Delphi 6 or Kylix” or “Delphi/Kylix” throughout the book, I use the generic term “Delphi,” which will serve to mean either Delphi 6 or Kylix. In the few cases where a statement applies only to Delphi 6 (VCL), I specifically point that out.

## Components Developed in This Book

Although this isn’t a book about component development, I have included four VCL-specific descendants of data-aware components that I think you will find useful. These components are discussed in Chapters 5 and 6. The source code for this book includes the Delphi package ETH, which includes the following components:

- **TETHDBComboBox**: A descendant of the data-aware component TDBComboBox that allows you to select an item from a combo box and store its index in an integer field.
- **TETHDBListBox**: A descendant of the data-aware component TDBListBox that allows you to select an item from a list box and store its index in an integer field.
- **TETHDBDateTimePicker**: A data-aware version of the Win32 component TDateTimePicker.
- **TETHDBGrid**: A descendant of TDBGrid that fires an event when the user resizes a column.

## Sample Applications

Each chapter in this book includes a number of sample applications to help you understand the concepts being discussed. The samples were all compiled and tested using Delphi 6—both the VCL and CLX versions.

The source code for the sample programs can be downloaded from http://www.sampublishing.com/detail_sams.cfm?item=067232265x6 or from my own Web site, located at http://www.tpx.turbopower.com/~Eric.Harmon. In the latter case, click the Books and Articles link, and then click the download link near the top of the page.

The following list provides a road map, by chapter, of the sample applications developed in this book.

### Chapter 1

- **Events**: Illustrates the different connection events fired by the TSQLConnection component.
- **MetaData**: Shows how to retrieve simple metadata information from a dbExpress connection.
- **DDLSQL**: Shows how to send DDL and SQL commands directly to a TSQLConnection component.
- **Trans**: Illustrates how transaction support works in dbExpress.
- **Feedback**: Shows how to provide feedback about what’s happening in a dbExpress connection.
