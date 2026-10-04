
# 9
## ZCLASSES

9.1 Why Use ZClasses? 158
9.1.1 Example ZClass Application: Bookstore 158
9.2 Classes and Objects 158
9.2.1 Creating a ZClass 160
9.2.2 Example: CorClass 160
9.2.3 Identification Numbers 160
9.2.4 Property Sheets 160
9.3 Creating a ZClass 161
9.3.1 Creating a Product 161
9.3.2 Adding a ZClass to the Product 162
9.3.3 The Create Constructor Objects Checkbox 164
9.3.4 Changing the ZClass Information 165
9.3.5 Base Classes and Their Views 168
9.3.6 Creating a Property Sheet and Properties 168
9.3.7 Creating a Selection or Multiple Selection Property 172
9.3.8 Establishing Views 173
9.3.9 Creating Help Topics 176
9.3.10 Editing Properties 178
Summary 178

# 10
## WORKING WITH THE ZCLASS

10.1 Modifying the Constructor Methods 179
10.1.1 Modifying DTML Methods 179
10.1.2 Creating Objects with ZClasses 184
10.1.3 The Book Class Factory 185
10.2 Running the Store 186
10.3 Two Ways to Edit Your Book Objects 186
10.3.1 Working in the Books Folder with the Management Screen 187
10.3.2 Working with an Administration Interface 187
10.3.3 Admin_html DTML Methods 190
10.4 Selling Your Books 197
10.4.1 Creating index_html 198
10.4.2 Creating the DTML Methods for Ordering Books 199
10.4.3 Sending the Order 202
10.5 Ideas for Expanding Your Zope Product 203
Summary 203

# 11
## THE ZCATALOG

11.1 Creating a ZCatalog 205
11.1.1 Creating a Vocabulary 206
11.1.2 Grabbing 206
11.2 The ZCatalog Screens 206
11.2.1 Contents Screen 207
11.2.2 The Catalog Screen 207
11.2.3 The Find Objects Screen 208
11.2.4 Metadata Screen 210
11.2.5 Indexes Screen 212
11.2.6 Advanced Screen 213
11.3 Z Search Interface 214
11.3.1 The Search Page 215
11.3.2 The Results Page 217
11.4 ZCatalog Queries 219
11.4.1 Querying ZCatalogs from a Frame 219
11.4.2 Catalog Brains 220
11.4.3 Querying Catalogs Directly 221
11.5 The Vocabulary 226
11.5.1 The Vocabulary Screen 226
11.5.2 Searching the Vocabulary 226
11.5.3 Expanding the Vocabulary: The insert() and manage_insert() Methods 227
11.5.4 ZCatalog with Special Characters 228
Summary 228

# 12
## ZOPE AND MYSQL

12.1 ZODB or External Database? 229
12.2 RDBMS 230
12.3 The MySQL Database 231
12.3.1 Starting MySQL Manager 231
12.3.2 Creating a Database with MySQL Manager 232
12.3.3 Creating the User Data Table with MySQL Manager 233
12.3.4 Installing the Database Adapter ZMySQLDA 234
12.3.5 Establishing a Z MySQL Connection in Zope 234
12.3.6 Testing SQL Queries to Your Database 235
12.4 Filling Tables with Data Using Zope 236
12.4.1 The UserAddform_html Method 237
12.4.2 The UserAdd_html Method 238
12.4.3 The UserInsert_sql Method 239
12.4.4 Testing Your SQL Methods 240
12.5 Querying the Database Using Zope 242
12.5.1 Creating SQL Methods for Search 242
12.5.2 The sqltest 243
12.5.3 The sqlvor Tool 244
12.6 Creating a Search Interface 245
12.6.1 Creating an Input Screen for the Search 245
Summary 247

# 13
## PROGRAMMING ZOPE: PYTHON IN A JIFFY

13.1 Data Types 250
13.1.1 Numeric Types 251
13.1.2 Sequential Types 252
13.1.3 None 255
13.2 Operators 255
13.3 Variables and Assignments 258
13.4 Indention 258
13.5 Classes and Methods 259
13.5.1 Example: Creating Class 259
Summary 262

# 14
## SCRIPTING ZOPE WITH PYTHON

14.1 Zope Python Scripts 263
14.1.1 Creating Python Scripts 264
14.1.2 Editing Screen 265
14.1.3 Binding Management Screen 265
14.1.4 Test Screen 266
14.1.5 Importing Modules into Python Scripts 266
14.1.6 Python Scripts from DTML 267
14.1.7 Example: Creating a Zope Python Script 268
14.1.8 Using the Script from DTML 269
14.2 External Methods 270
14.2.1 Creating External Methods 270
14.2.2 Accessing Python Methods with DTML 272
14.2.3 Example: Creating an External Method 272
14.2.4 Creating an External Object in Zope 273
14.2.5 Summary of External Methods 274
14.3 Using Methods to Change Roles and Permissions 274
14.3.1 Creating Permissions for Multiple Roles 274
14.3.2 permission_settings() 275
14.3.3 The Permission Method-by-Step 276
14.3.4 Using the permissions.py Method 277
14.3.5 The createUser() Method 278
Summary 278

# 15
## ZOPE PRODUCTS

15.1 Tool for Creating Objects 282
15.2 Constructing a Product 282
15.2.1 Bootstrapping the Product 283
15.2.2 Necessary Components 283
15.2.3 User Structure 284
15.2.4 Roles/Permissions Structure 284
15.3 Product Construction at a Glance 285
15.3.1 Major Components 285
15.3.2 Support Files 286
15.3.3 Putting It All 286
15.4 Creating the Website Product 286
15.4.1 Create the Product Directory 287
15.4.2 The Main Module: Website.py 289
15.4.3 Defining the Constructor Form 299
15.4.4 The Constructor Method of the Main Module 300
15.4.5 Writing the __init__.py File 305
Summary 308

# 16
## DEBUGGING

16.1 Errors When Starting the Zope 309
16.2 Python and DTML Errors 310
16.2.1 Binary Searching 310
16.2.2 Defensive Coding 311
16.2.3 Intermittent Errors 312
16.2.4 Standard Python Error Messages 312
16.2.5 DTML Error Messages 312
16.2.6 Debug Mode 314
16.3 Errors Specific to Zope 315
16.3.1 Zope Error Messages 315
Summary 322

# 17
## EXTERNAL DATA ACCESS

17.1 FTP 323
17.1.1 Using Graphical FTP 325
17.2 WebDAV 326
17.2.1 WebDAV for Linux and Unix 328
17.3 XML-RPC 328
Summary 332

## A
DTML AND BUILT-IN ATTRIBUTES

A.1 The var Tag 333
A.1.1 Special Forms 337
A.2 The Namespace Variable 338
A.2.1 Modules 340
A.2.2 Client-Server Communication 344

## B
THE REQUEST OBJECT

REQUEST 355

## C
SOURCE CODE FOR THE WEBSITE PRODUCT

C.1 Source Text for __init__.py for the Website Product 359
C.2 Source Text for Website.py for the Website Product 360
C.2.1 WebsiteForm.dtml 365
C.3 The DTML Methods for the Website Product 366
C.3.1 WebsiteUsers_list.dtml 366
C.3.2 edit_WebsiteUser.dtml 366
C.3.3 index_html.dtml 368
C.3.4 login_html.dtml 368
C.3.5 new_WebsiteUser.dtml 368
C.3.6 products_html.dtml 369
C.3.7 order_html_footer.dtml 369
C.3.8 order_html_header.dtml 370
C.3.9 about_us_html.dtml 371

## D
SOME ZCATALOG MODULE METHODS 373

## E
GLOSSARY 379

## Index 383

# PREFACE

## Who Is This Book For?

We have designed this book as an introduction to Zope for beginners, and as a more complete reference for experienced users. We hope that it makes getting to know Zope much easier for you and that it will form the basis for your productive work with Zope. The following will be both beneficial and important, especially for later chapters:

- HTML knowledge is helpful.
- Python knowledge is necessary for later chapters.

This book stems from our Zope documentation (marketed as E-Books in English and German throughout the world—visit www.behive.de for more information). The E-Books deal only with individual aspects of Zope, but this book will describe and explain all of the fundamental characteristics and technologies of the Zope system.

## What Version of Zope Does It Cover?

This book deals with versions of Zope through 2.3. As such, we recommend you start with Zope 2.3 or earlier and use this book as your guide.
