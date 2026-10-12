
# About This eBook

ePUB is an open, industry-standard format for eBooks. However, support of ePUB and its many features varies across reading devices and applications. Use your device or app settings to customize the presentation to your liking. Settings that you can customize often include font, font size, single or double column, landscape or portrait mode, and figures that you can click or tap to enlarge. For additional information about the settings and features on your reading device or app, visit the device manufacturer’s Web site.

Many titles include programming code or configuration examples. To optimize the presentation of these elements, view the eBook in single-column, landscape mode and adjust the font size to the smallest setting. In addition to presenting code and configurations in the reflowable text format, we have included images of the code that mimic the presentation found in the print book; therefore, where the reflowable format may compromise the presentation of the code listing, you will see a “Click here to view code image” link. Click the link to view the print-fidelity code image. To return to the previous page viewed, click the Back button on your device or app.

## Programming in C

Fourth Edition

Stephen G. Kochan

Addison-Wesley

- Upper Saddle River, NJ
- Boston
- Indianapolis
- San Francisco
- New York
- Toronto
- Montreal
- London
- Munich
- Paris
- Madrid
- Cape Town
- Sydney
- Tokyo
- Singapore
- Mexico City

### Programming in C, Fourth Edition

Copyright © 2015 by Pearson Education, Inc.

All rights reserved. No part of this book shall be reproduced, stored in a retrieval system, or transmitted by any means, electronic, mechanical, photocopying, recording, or otherwise, without written permission from the publisher. No patent liability is assumed with respect to the use of the information contained herein. Although every precaution has been taken in the preparation of this book, the publisher and author assume no responsibility for errors or omissions. Nor is any liability assumed for damages resulting from the use of the information contained herein.

ISBN 13: 978-0-321-77641-9

ISBN 10: 0-321-77641-0

Library of Congress Control Number: 2014944082

Printed in the United States of America

First Printing: August 2014

**Acquisitions Editor**
Mark Taber

**Managing Editor**
Sandra Schroeder

**Project Editor**
Mandie Frank

**Copy Editor**
Charlotte Kughen

**Indexer**
Brad Herriman

**Proofreader**
Debbie Williams

**Technical Editor**
Siddhartha Singh

**Editorial Assistant**
Vanessa Evans

**Designer**
Chuti Prasertsith

**Composer**
Mary Sudul

**Trademarks**
All terms mentioned in this book that are known to be trademarks or service marks have been appropriately capitalized. The publisher cannot attest to the accuracy of this information. Use of a term in this book should not be regarded as affecting the validity of any trademark or service mark.

### Warning and Disclaimer

Every effort has been made to make this book as complete and as accurate as possible, but no warranty or fitness is implied. The information provided is on an "as is" basis. The author and the publisher shall have neither liability nor responsibility to any person or entity with respect to any loss or damages arising from the information contained in this book.

### Special Sales

For information about buying this title in bulk quantities, or for special sales opportunities (which may include electronic versions; custom cover designs; and content particular to your business, training goals, marketing focus, or branding interests), please contact our corporate sales department at corpsales@pearsoned.com or (800) 382-3419.

For government sales inquiries, please contact governmentsales@pearsoned.com.

For questions about sales outside the U.S., please contact international@pearsoned.com.

## Developer’s Library

ESSENTIAL REFERENCES FOR PROGRAMMING PROFESSIONALS

*Developer’s Library* books are designed to provide practicing programmers with unique, high-quality references and tutorials on the programming languages and technologies they use in their daily work. All books in the *Developer’s Library* are written by expert technology practitioners who are especially skilled at organizing and presenting information in a way that’s useful for other programmers.

Key titles include some of the best, most widely acclaimed books within their topic areas:

- *Programming in Objective-C*
  Stephen G. Kochan
  ISBN 978-0-321-96760-2
- *MySQL*
  Paul DuBois
  ISBN-13: 978-0-321-83387-7
- *Linux Kernel Development*
  Robert Love
  ISBN-13: 978-0-672-32946-3
- *Python Essential Reference*
  David Beazley
  ISBN-13: 978-0-672-32978-4
- *PostgreSQL*
  Korry Douglas
  ISBN-13: 978-0-672-32756-8
- *C++ Primer Plus*
  Stephen Prata
  ISBN-13: 978-0-321-77640-2

Developer’s Library books are available in print and in electronic formats at most retail and online bookstores, as well as by subscription from Safari Books Online at **safari.informit.com**

**Developer’s Library**
[informit.com/devlibrary](informit.com/devlibrary)

For my mother and father

## Contents at a Glance

- Introduction
- 1 Some Fundamentals
- 2 Compiling and Running Your First Program
- 3 Variables, Data Types, and Arithmetic Expressions
- 4 Program Looping
- 5 Making Decisions
- 6 Working with Arrays
- 7 Working with Functions
- 8 Working with Structures
- 9 Character Strings
- 10 Pointers
- 11 Operations on Bits
- 12 The Preprocessor
- 13 Extending Data Types with the Enumerated Data Type, Type Definitions, and Data Type Conversions
- 14 Working with Larger Programs
- 15 Input and Output Operations in C
- 16 Miscellaneous and Advanced Features
- 17 Debugging Programs
- 18 Object-Oriented Programming
- A C Language Summary
- B The Standard C Library
- C Compiling Programs with gcc
- D Common Programming Mistakes
- E Resources
- Index

## Table of Contents

1. Introduction
   - Programming
   - Higher-Level Languages
   - Operating Systems
   - Compiling Programs
   - Integrated Development Environments
   - Language Interpreters
2. 1 Some Fundamentals
3. 2 Compiling and Running Your First Program
   - Compiling Your Program
   - Running Your Program
   - Understanding Your First Program
   - Displaying the Values of Variables
   - Comments
   - Exercises
4. 3 Variables, Data Types, and Arithmetic Expressions
   - Understanding Data Types and Constants
     - The Integer Type int
     - The Floating Number Type float
     - The Extended Precision Type double
     - The Single Character Type char
     - The Boolean Data Type
     - Type Specifiers: l, ll, s, u, and z
   - Working with Variables
   - Working with Arithmetic Expressions
     - Integer Arithmetic and the Unary Minus Operator
     - Combining Operations with Assignment: The Assignment Operators
   - Types and Operators
   - Exercises
5. 4 Program Looping
   - Triangular Numbers
   - The for Statement
   - Relational Operators
   - Aligning Output
   - Program Input
     - Nested for Loops
     - for Loop Variants
   - The while Statement
   - The do...while Statement
   - The break Statement
   - The continue Statement
   - Exercises
6. 5 Making Decisions
   - The if Statement
     - The else Construct
       - Compound Relational Tests
       - Nested if Statements
       - The switch Construct
   - The switch Statement
   - Boolean Variables
   - The Conditional Operator
   - Exercises
7. 6 Working with Arrays
   - Defining an Array
     - Using Array Elements as Counters
     - Generating Fibonacci Numbers
     - Using an Array to Generate Prime Numbers
   - Initializing Arrays
   - Character Arrays
     - Base Conversion Using Arrays
     - The const Qualifier
   - Multidimensional Arrays
   - Variable Length Arrays
   - Exercises
8. 7 Working with Functions
   - Defining a Function
   - Arguments and Local Variables
