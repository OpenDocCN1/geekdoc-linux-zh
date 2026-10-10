
## Credits

**Acquisitions Editor**  
Laura Lewin

**Development Editors**  
Kathi Duggan  
Andy Markinkovich

**Technical Editor**  
Jason Luster

**Copy Editors**  
Victoria Lee  
Mildred Sanchez

**Project Coordinators**  
Linda Marousek  
Marcos Vergara

**Quality Control Specialists**  
Laura Talfinger  
Chris Weisbart

**Graphics and Production Specialists**  
Robert Bihlmayer  
Jude Levinson  
Michael Lewis

**Book Designer**  
Drew R. Moore

**Illustrator**  
Mary Jo Richards  
Karl Brandt

**Proofreading and Indexing**  
York Production Services

**Cover Illustration Design**  
Peter Kowaleszyn, *Murder By Design*, San Francisco

## About the Author

Arthur Griffith has been programming computers for 25 years. He has several years of experience in graphics programming, including X11 and Motif. His broad experience includes oil and gas monitoring, satellite communications, insurance company databases, real-time controls, and hardware diagnostic systems. He specializes in writing computer language interpreters and compilers and has implemented several special-purpose languages. Among the books he has written are *Java Master Reference* and *COBOL For Dummies*. He is also the co-author of *Peter Norton's Complete Guide to Linux*. Arthur lives in Homer, Alaska, and is now a full-time writer. You can contact him at arthur@belugalake.com.

## Preface

*For Mary*

## In This Book

The first two chapters of this book provide an overview of the book's contents and the overall structure of the C++ language. The first chapter explains the book's organization, while the second chapter outlines the book's contents and how they are organized.

The second part of the book is organized around the concept of objects, classes, and functions. This part covers the core features of C++, including basic programming elements, functions, and classes. It also explores more advanced topics such as inheritance and polymorphism.

The final part of the book focuses on advanced topics in C++, including templates, exceptions, and the Standard Template Library (STL). This part also covers topics such as file input/output, multithreading, and the integration of C++ with other languages.

## What You Will Need

To get the most out of this book, you'll need a C++ compiler that supports C++11 or later. The examples in this book are compatible with most modern C++ compilers, including GCC, Clang, and MSVC. Additionally, you'll need a text editor or IDE that supports C++ syntax highlighting and debugging features.

## Subject to Change

Language standards are subject to change. While the content of this book is based on the latest C++ standards, future revisions may include updates or modifications. Always refer to the latest standard documents for the most accurate information.

## Credits

- **Creative Director**
- **Design Director**
- **Art Director**
- **Managing Editor**
- **Assistant Editor**
- **Senior Editorial Assistant**
- **Production Manager**
- **Copy Chief**
- **Copy Editor**
- **Project Manager**
- **Managing Editor**
- **Marketing Manager**
- **Senior Marketing Manager**
- **Production Supervisor**
- **Project Management**
- **Design Assistant**
- **Design Director**
- **Production Manager**
- **Managing Editor**
- **Assistant Editor**
- **Managing Editor**
- **Copy Chief**
- **Copy Editor**
- **Senior Editorial Assistant**
- **Production Supervisor**
- **Senior Marketing Manager**
- **Production Manager**
- **Project Management**
- **Design Assistant**

## About the Author

This book is written for the purpose of sharing the knowledge and experience gained from many years of teaching and working with the general public. It is intended to be a practical guide that will help the reader to understand and apply the concepts discussed. The author believes that by providing clear explanations and practical examples, readers will be able to make informed decisions and improve their outcomes.

## Preface

## In This Book

If you want to write a GNOME application, you’ve come to the right book.

This book is composed of one example program after another, and each example is accompanied by an explanation. Each example is also a complete running program designed to demonstrate just one thing.

My personal preference, when exploring or learning something new about software, is to have a simple example that shows me just what I want and nothing else. Software is complicated enough that it becomes impossible to explain all the nuances without showing an example, and an example can be very confusing unless the key parts of it are explained.

The documentation of a program can be included as comments in the code, or it can be separate text supplied along with the code. The examples in this book have no embedded comments because each one is accompanied by text that explains it. Leaving out comments produces a cleaner format that makes it easier for a reader to see the structure of the program. Most of the code is printed in the book with line numbers so the explanations can refer to specific lines.

## What You Will Need

If you know how to program in C, have access to a Linux computer, and are able to download files from the Internet, this book will supply you with the know-how you need to write GNOME applications.

There is a version of the development software on the CD, which is described in Appendix A. Alternatively, see Appendix B to get the latest version of everything. Appendix B contains a list of all the software you will need, and where it can be found on the Internet.

## Subject to Change

GNOME is large, powerful, and moving fast. Fortunately, it is also very friendly.

GNOME is an ongoing project. New things are being added constantly. Because of its open source status, this growth will probably continue for the life of GNOME and GTK+.

From time to time new methods for getting things done will be added, and it is possible that some of the techniques described in this book will become outdated. But everything in the book should continue to work. Being deprecated is not the same as being obsolete — the old function calls will still work, it’s just that a new (and hopefully better) way of doing it will have been added. In some cases, there may be output during the compile stating that some function or other has been deprecated — this is so you can take the opportunity to upgrade your program to a new way of doing things.

### How to Use This Book

The book is divided into three parts. The first part is one continuous tutorial covering the basics of GNOME/GTK+ programming. The second part is also comprised of tutorials, but the chapters can be taken on order on an as-needed basis. The third part is not intended to be read sequentially — it is more of a reference section, as are Appendices C through G.

### Appendix A or B: Installing the Software

If you have a late model Linux on a CD, you will have most of the software and may have it all. If not, you have two options. You can install it from the CD supplied with this book, or you can retrieve it from the Internet. Appendix A discusses the CD and Appendix B discusses the Internet.

### Chapter 24: From Win32 to Gnome

If you are a Win32 programmer, start by reading Chapter 24. This chapter is a point-by-point comparison of two programs — one written for Win32 and the other written for GNOME. There are some basic differences, but the underlying concepts behind writing a GNOME application are very much like those behind writing a Win32 application.

### Part I: Getting Started

This part of the book starts from the very beginning and puts the pieces together until you are able to create applications that display buttons, labels, and other widgets with whatever size, shape, and position you would like them to be. The first chapter explains some of the background information — mostly having to do with the libraries available and the structure of GNOME and GTK+ code.
