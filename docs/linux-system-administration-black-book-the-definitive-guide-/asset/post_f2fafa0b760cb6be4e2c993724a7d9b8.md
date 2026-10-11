
![](img/e612d46dba3c9205aa19fee9eb8dd0a4_0_0.png)

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_0_1.png)

CORIOLIS OPEN PRESS

# LINUX

## System Administration

### Black Book

Comprehensive Problem Solver

Ann LeBlanc

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_0_2.png)

# Linux System Administration Black Book

Dee-Ann LeBlanc

CORIOLIS

# Copyright

© 2000 Dee-Ann LeBlanc. All rights reserved.

This book may not be duplicated in any way without the express written consent of the publisher, except in the form of brief excerpts or quotations for the purpose of review. The information contained herein is for the personal use of the reader and may not be incorporated in any commercial programs, other books, databases, or any kind of software without written consent of the publisher. Making copies of this book or any portion for any purpose other than your own is a violation of United States copyright laws.

## Limits of Liability and Disclaimer of Warranty

The author and publisher of this book have used their best efforts in preparing the book and the programs contained in it. These efforts include the development, research, and testing of the theories and programs to determine their effectiveness. The author and publisher make no warranty of any kind, expressed or implied, with regard to these programs or the documentation contained in this book.

The author and publisher shall not be liable in the event of incidental or consequential damages in connection with, or arising out of, the furnishing, performance, or use of the programs, associated instructions, and/or claims of productivity gains.

## Trademarks

Trademarked names appear throughout this book. Rather than list the names and entities that own the trademarks or insert a trademark symbol with each mention of the trademarked name, the publisher states that it is using the names for editorial purposes only and to the benefit of the trademark owner, with no intention of infringing upon that trademark.

The Coriolis Group, LLC
14455 N. Hayden Road
Suite 220
Scottsdale, Arizona 85260

(480) 483-0192
FAX (480) 483-0193
www.coriolis.com

**Library of Congress Cataloging-in-Publication Data**

LeBlanc, Dee-Ann
Linux system administration black book / by Dee-Ann LeBlanc
p. cm.
ISBN 1-57610-419-2
1. Linux. 2. Operating systems (Computers). I. Title.
QA76.76.O63 L4325 2000
004.4'96-dc21

Printed in the United States of America
10 9 8 7 6 5 4 3 2 1

00-043141
CIP

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_4_0.png)

Dear Reader:

Coriolis Technology Press was founded to create a very elite group of books: the ones you keep closest to your machine. Sure, everyone would like to have the Library of Congress at arm's reach, but in the real world, you have to choose the books you rely on every day very carefully.

To win a place for our books on that coveted shelf beside your PC, we guarantee several important qualities in every book we publish. These qualities are:

-   *Technical accuracy*—It's no good if it doesn't work. Every Coriolis Technology Press book is reviewed by technical experts in the topic field, and is sent through several editing and proofreading passes in order to create the piece of work you now hold in your hands.
-   *Innovative editorial design*—We've put years of research and refinement into the ways we present information in our books. Our books' editorial approach is uniquely designed to reflect the way people learn new technologies and search for solutions to technology problems.
-   *Practical focus*—We put only pertinent information into our books and avoid any fluff. Every fact included between these two covers must serve the mission of the book as a whole.
-   *Accessibility*—The information in a book is worthless unless you can find it quickly when you need it. We put a lot of effort into our indexes, and heavily cross-reference our chapters, to make it easy for you to move right to the information you need.

Here at The Coriolis Group we have been publishing and packaging books, technical journals, and training materials since 1989. We're programmers and authors ourselves, and we take an ongoing active role in defining what we publish and how we publish it. We have put a lot of thought into our books; please write to us at ctp@coriolis.com and let us know what you think. We hope that you're happy with the book in your hands, and that in the future, when you reach for software development and networking information, you'll turn to one of our books first.

Keith Weiskamp
President and CEO

Jeff Duntemann
VP and Editorial Director

## Look for these related books from The Coriolis Group:

**Linux Install and Configuration Little Black Book**
*by Dee-Ann LeBlanc and Isaac-Hajime Yates*

**Linux IP Stacks Commentary**
*by Stephen Satcell and HBJ Clifford*

**Linux Core Kernel Commentary**
*by Scott A. Maxwell*

**Setting Up a Linux Internet Server**
*by Hidenori Tsuji, Takashi Watanabe, and Acrobyte*

**Setting Up a Linux Intranet Server**
*by Hidenori Tsuji, Takashi Watanabe, and Acrobyte*

**Linux Graphics Programming with SVGAlib**
*by Jay Link*

## Also recently published by Coriolis Open™ Press:

**Samba Black Book**
*by Dominic Baines*

**Open Source Development with CVS**
*by Karl Franz Fogel*

*I dedicate this book to my friend Andrew,*
*who helps me stay sane during crunch times.*

## About The Author

**Dee-Ann LeBlanc** is a computer book author, course developer, and technical trainer specializing in Linux. She has done several books on the subject, including *Linux Install and Configuration Little Black Book* and *General Linux I Exam Prep* for The Coriolis Group, and writes a monthly column on integrating Linux with other operating systems for *Linux AppDev*. Dee-Ann is both a Red Hat Certified Engineer and a SAI/GNU Linux Certified Professional who teaches Linux, Unix, and other courses for two different online schools, presents the occasional seminar at computer conferences, and develops courses for a number of online venues.

In her copious spare time, Dee-Ann works on a medieval fantasy novel, is walked by her dog Zorro, and squeezes in a few minutes to spend time with her husband Rob and see the beautiful scenery in BC, Canada.

## Acknowledgments

I would first like to acknowledge all of the staff at The Coriolis Group who worked so hard to make this project a success: Toni Zuccarini Ackley, William McManus, David Williams, Meg Turecek, Michelle McConnell, and Jody Winkler. I would also like to thank the students who keep me on my toes and are constantly giving me great ideas for things to include, and the readers who contact me to let me know what they liked and didn’t like about my various books, and what they would like to see included in later projects.

# Contents At A Glance

-   Chapter 1 Red Hat Linux 1
-   Chapter 2 User Management 21
-   Chapter 3 File System Management 59
-   Chapter 4 Package Management 101
-   Chapter 5 Kernel Management 125
-   Chapter 6 GUI Management 151
-   Chapter 7 Networking 171
-   Chapter 8 Printing 217
-   Chapter 9 System Security Basics 239
-   Chapter 10 KickStart For Repeat Installations 293
-   Chapter 11 DNS With BIND 315
-   Chapter 12 Internet Email: sendmail + IDA 351
-   Chapter 13 The Apache Web Server 407
-   Chapter 14 The Squid Internet Object Cache 453
-   Chapter 15 FTP And Telnet 475
-   Chapter 16 NIS And NIS+ 491
-   Chapter 17 NFS 501
-   Chapter 18 Samba 511
-   Chapter 19 Text Processing Tools 561
-   Chapter 20 Shell Scripting 597
-   Chapter 21 Perl Scripting 627
-   Chapter 22 Linux C Programming 643
-   Chapter 23 Additional System Administration Tools 659
-   Appendix GNU General Public License 687
