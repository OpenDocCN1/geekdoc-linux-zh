
# Absolute FreeBSD

THE COMPLETE GUIDE TO FREEBSD

MICHAEL W. LUCAS

![](img/f11aeb3fa2ed406688e13ccb43ed9dab_0_0.png)

3RD EDITION

![](img/f11aeb3fa2ed406688e13ccb43ed9dab_0_1.png)

![](img/f11aeb3fa2ed406688e13ccb43ed9dab_1_0.png)

# Absolute FreeBSD

THE COMPLETE GUIDE TO FREEBSD

MICHAEL W. LUCAS

![](img/f11aeb3fa2ed406688e13ccb43ed9dab_1_1.png)

# 3RD EDITION

no starch press

## PRAISE FOR ABSOLUTE FREEBSD

> “Even longtime users of FreeBSD may be surprised at the power and features it can bring to bear as a server platform, and *Absolute FreeBSD* is an excellent guide to harnessing that power.”
> —UNIXREVIEW.COM

> “ . . . provides beautifully written tutorials and reference material to help you make the most of the strengths of this OS.”
> —LINUXUSER & DEVELOPER MAGAZINE

> “ . . . packed with a lot of information.”
> —DAEMON NEWS

> “When was the last time you could physically feel yourself getting smarter while reading a book? If you are a beginning to average FreeBSD user, *Absolute FreeBSD* . . . will deliver that sensation in spades.”
> —RICHARD BEJTLICH, TAO SECURITY

> “By far the best FreeBSD book I have ever owned is *Absolute FreeBSD*, 2nd Edition by No Starch Press.”
> —BSD ZEALOT

> “Master practitioner Lucas organizes features and functions to make sense in the development environment, and so provides aid and comfort to new users, novices, and those with significant experience alike.”
> —SCITECH BOOK NEWS

## ABSOLUTE FREEBSD®

3RD EDITION

### The Complete Guide to FreeBSD

by Michael W. Lucas

![](img/f11aeb3fa2ed406688e13ccb43ed9dab_3_0.png)

San Francisco

ABSOLUTE FREEBSD®, 3RD EDITION. Copyright © 2019 by Michael W. Lucas.
All rights reserved. No part of this work may be reproduced or transmitted in any form or by any means, electronic or mechanical, including photocopying, recording, or by any information storage or retrieval system, without the prior written permission of the copyright owner and the publisher.

ISBN-10: 1-59327-892-6
ISBN-13: 978-1-59327-892-2

Publisher: William Pollock
Production Editor: Janelle Ludowise
Cover and Interior Design: Octopod Studios
Developmental Editor: William Pollock
Technical Reviewers: John Baldwin, Benno Rice, and George V. Neville-Neil
Copyeditor: Julianne Jigour
Composer: Susan Glinert Stevens
Proofreader: James Fraleigh
Indexer: Nancy Guenther

For information on distribution, translations, or bulk sales, please contact No Starch Press, Inc. directly:
No Starch Press, Inc.
245 8th Street, San Francisco, CA 94103
phone: 1.415.863.9900; info@nostarch.com
www.nostarch.com

## Library of Congress Cataloging-in-Publication Data

Lucas, Michael, 1967-
Absolute FreeBSD : the complete guide to FreeBSD / Michael W. Lucas. -- 2nd ed.
p. cm.
Includes index.
ISBN-13: 978-1-59327-151-0
ISBN-10: 1-59327-151-4
1. FreeBSD. 2. UNIX (Computer file) 3. Internet service providers--Computer programs. 4. Web servers--Computer programs. 5. Client/server computing. I. Title.
QA76.76.063L83 2007
004' .36- -dc22

2007036190

No Starch Press and the No Starch Press logo are registered trademarks of No Starch Press, Inc. Other product and company names mentioned herein may be the trademarks of their respective owners. Rather than use a trademark symbol with every occurrence of a trademarked name, we are using the names only in an editorial fashion and to the benefit of the trademark owner, with no intention of infringement of the trademark.

The information in this book is distributed on an “As Is” basis, without warranty. While every precaution has been taken in the preparation of this work, neither the author nor No Starch Press, Inc. shall have any liability to any person or entity with respect to any loss or damage caused or alleged to be caused directly or indirectly by the information contained in it.

## About the Author

After using Unix since the late '80s and spending twenty-odd years as a network and system administrator specializing in building and maintaining high-availability systems, Michael W. Lucas now writes about them for a living. He's written more than 30 books, which have been translated into nine languages. His critically acclaimed titles include *Absolute OpenBSD*, *Cisco Routers for the Desperate*, and *PGP & GPG*, all from No Starch Press. Learn more at [https://mwl.io/](https://mwl.io/).

## About the Technical Reviewers

**John Baldwin** joined the FreeBSD Project as a committer in 1999. He has worked in several areas of the system, including SMP infrastructure, the network stack, virtual memory, and device driver support. John has served on the Core and Release Engineering teams and organized several FreeBSD developer summits.

**Benno Rice** has been using FreeBSD since 1995 and has been a committer since 2000 when he started the PowerPC port. Since then he has worked in a variety of areas and for a number of FreeBSD-using companies. He has also served on the Core Team and presented on FreeBSD-related topics at several conferences.

**George V. Neville-Neil** works on networking and operating system code for fun and profit. His areas of interest are code spelunking, operating systems, networking, and time protocols. He is the co-author with Marshall Kirk McKusick and Robert N. M. Watson of *The Design and Implementation of the FreeBSD Operating System* (Addison-Wesley Professional, 2004).

## BRIEF CONTENTS

- Foreword by Marshall Kirk McKusick
- Acknowledgments
- Introduction
- Chapter 1: Getting More Help
- Chapter 2: Before You Install
- Chapter 3: Installing
- Chapter 4: Start Me Up! The Boot Process
- Chapter 5: Read This Before You Break Something Else! (Backup and Recovery)
- Chapter 6: Kernel Games
- Chapter 7: The Network
- Chapter 8: Configuring Networking
- Chapter 9: Securing Your System
- Chapter 10: Disks, Partitioning, and GEOM
- Chapter 11: The Unix File System
- Chapter 12: The Z File System
- Chapter 13: Foreign Filesystems
- Chapter 14: Exploring /etc
- Chapter 15: Making Your System Useful
- Chapter 16: Customizing Software with Ports
- Chapter 17: Advanced Software Management
- Chapter 18: Upgrading FreeBSD
- Chapter 19: Advanced Security Features
- Chapter 20: Small System Services
- Chapter 21: System Performance and Monitoring
- Chapter 22: Jails
- Chapter 23: The Fringe of FreeBSD
- Chapter 24: Problem Reports and Panics
- Afterword
- Bibliography
- Index

## CONTENTS IN DETAIL

**FOREWORD** by Marshall Kirk McKusick

**ACKNOWLEDGMENTS**

**INTRODUCTION**

- What Is FreeBSD?
  - BSD: FreeBSD’s Granddaddy
  - The BSD License
  - The AT&T/CSRG/BSDi Iron Cage Match
  - The Birth of FreeBSD
- FreeBSD Development
  - Committers
  - Contributors
  - Users
- Other BSDs
  - NetBSD
  - OpenBSD
  - DragonFly BSD
  - macOS
  - FreeBSD’s Children
- Other Unixes
  - Solaris
  - illumos
  - AIX
  - Linux
  - Other Unixes
- FreeBSD’s Strengths
  - Portability
  - Power
  - Simplified Software Management
  - Customizable Builds
  - Advanced Filesystems
- Who Should Use FreeBSD?
- Who Should Run Another BSD?
- Who Should Run a Proprietary Operating System?
- How to Read This Book
- What Must You Know?
- For the New System Administrator
  - Desktop FreeBSD
  - How to Think About Unix
- Notes on the Third Edition
- Contents of This Book

### 1. GETTING MORE HELP

- Why Not Beg for Help?
  - The FreeBSD Attitude
  - Support Options
- Man Pages
  - Manual Sections
  - Navigating Man Pages
  - Finding Man Pages
  - Section Numbers and Man
  - Man Page Contents
- FreeBSD.org
  - Web Documents
  - The Mailing List Archives
  - The Forums
- Other Websites
- Using FreeBSD Problem-Solving Resources
  - Checking the Handbook and FAQ
  - Checking the Man Pages
  - Mailing Lists Archives and Forums
