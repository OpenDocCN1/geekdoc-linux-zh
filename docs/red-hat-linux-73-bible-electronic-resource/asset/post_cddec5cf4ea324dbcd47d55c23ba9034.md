
## **100%**
### ONE HUNDRED PERCENT COMPREHENSIVE AUTHORITATIVE WHAT YOU NEED

“One Hundred Percent”

“The best overall Red Hat user’s book, hands down, no contest.”
—Al Stevens, C Programming Columnist, Dr. Dobb’s Journal, on a previous edition

- **Master** new techniques for installation, network configuration, and server setup
- **Discover** material on iptables firewall setup, DNS servers, wireless Linux LAN, WINE, and more
- **Explore** print and mail service switching, vsFTP server configuration, and other new features

# Red Hat® Linux® 7.3 Bible
**3 BONUS CD-ROMS**
with Red Hat Linux 7.3!

Christopher Negus

## Red Hat® Linux® 7.3 Bible
Christopher Negus

![](img/1744bde8c889adfab3fc911e1687fecf_2_0.png)

Wiley Publishing, Inc.

Best-Selling Books • Digital Downloads • e-Books • Answer Networks • e-Newsletters • Branded Web Sites • e-Learning

## Red Hat® Linux® 7.3 Bible

**Published by**
**Wiley Publishing, Inc.**
605 Third Avenue
New York, NY 10158
www.wiley.com

This book is printed on acid-free paper.

Copyright © 2002 by Wiley Publishing, Inc. All rights reserved.

Published by Wiley Publishing, Inc., Indianapolis, Indiana
Published simultaneously in Canada

No part of this publication may be reproduced, stored in a retrieval system or transmitted in any form or by any means, electronic, mechanical, photocopying, recording, scanning or otherwise, except as permitted under Sections 107 or 108 of the 1976 United States Copyright Act, without either the prior written permission of the Publisher, or authorization through payment of the appropriate per-copy fee to the Copyright Clearance Center, 222 Rosewood Drive, Danvers, MA 01923, (978) 750-8400, fax (978) 750-4744. Requests to the Publisher for permission should be addressed to the Legal Department, Wiley Publishing, Inc., 10475 Crosspoint Blvd., Indianapolis, IN 46256, (317) 572-3447, fax (317) 572-4447, E-Mail: permcordinator@wiley.com.

**Limit of Liability/Disclaimer of Warranty:** While the publisher and author have used their best efforts in preparing this book, they make no representations or warranties with respect to the accuracy or completeness of the contents of this book and specifically disclaim any implied warranties of merchantability or fitness for a particular purpose. No warranty may be created or extended by sales representatives or written sales materials. The advice and strategies contained herein may not be suitable for your situation. You should consult with a professional where appropriate. Neither the publisher nor author shall be liable for any loss of profit or any other commercial damages, including but not limited to special, incidental, consequential, or other damages.

For general information on our other products and services or to obtain technical support, please contact our Customer Care Department within the U.S. at 800-762-2974, outside the U.S. at 317-572-3993 or fax 317-572-4002.

Wiley also publishes its books in a variety of electronic formats. Some content that appears in print may not be available in electronic books.

Wiley and the Wiley Publishing logo are trademarks or registered trademarks of Wiley Publishing, Inc. in the United States and other countries and may not be used without written permission. Red Hat is a registered trademark or trademark of Red Hat, Inc. Linux is a trademark or registered trademark of Linus Torvalds. All other trademarks are the property of their respective owners. Wiley is not associated with any product or vendor mentioned in this book.

**Library of Congress Control Number:** 2002103272

ISBN: 0-7645-4941-3

Printed in the United States of America.

10 9 8 7 6 5 4 3 2 1
1B/RU/QW/QS/IN

## About the Author

**Christopher Negus** has been working with UNIX systems, the Internet, and (more recently) Linux systems for more than two decades. During that time, Chris worked at AT&T Bell Laboratories, UNIX System Laboratories, and Novell, helping to develop the UNIX operating system. Features from many of the UNIX projects Chris worked on at AT&T have found their way into Red Hat and other Linux systems.

During the past few years, Chris has written several books on UNIX and the Internet, including *Caldera OpenLinux Bible, Internet Explorer 4 Bible*, and *Netscape Plug-ins For Dummies* for Wiley Publishing. He also co-wrote several books for Que Corporation, including *The Complete Idiot's Guide to Networking* (second and third editions) and *Using UNIX* (second edition). Chris's other writings include articles for *Internet World, NetWare Connection*, and *Visual Developer* magazines.

At home, Chris enjoys spending time with his wife, Sheree, and his boys, Caleb and Seth. His hobbies include soccer, singing, and exercising with Sheree.

## Credits

- **Acquisitions Editor**
  - Debra Williams Cauley
- **Project Editor**
  - Neil Romanosky
- **Technical Editor**
  - Jason Luster
- **Copy Editors**
  - S. B. Kleinman
  - William A. Barton
- **Editorial Manager**
  - Mary Beth Wakefield
- **Vice President and Executive Group Publisher**
  - Richard Swadley
- **Vice President and Executive Publisher**
  - Bob Ipsen
- **Vice President and Publisher**
  - Joseph B. Wikkert
- **Executive Editorial Director**
  - Mary Bednarek
- **Project Coordinator**
  - Ryan Steffen
- **Proofreading**
  - Kim Cofer
- **Indexing**
  - Johanna VanHoose Dinse

I dedicate this book to my wife, Sheree. This book would never have happened without her love and support.

![](img/1744bde8c889adfab3fc911e1687fecf_7_0.png)

Digitized by the Internet Archive
in 2017 with funding from
Kahle/Austin Foundation

https://archive.org/details/redhatlinux73bib00chri

## Preface

Many Linux books resemble someone’s throwing a bunch of high-performance car parts on the floor and saying, “Go ahead and build a Porsche.” Although it’s true that the parts you need for power computing are in Linux, you still need to know how to put them together. Red Hat Linux 7.3 Bible takes you through those steps.

### Who Are You?

To use this book, you don’t have to be a programmer. You could be someone who just wants to use Red Hat Linux (to run programs, access the Internet, and so on). Or you may want to know how to administer a Linux system in a workgroup or on a network.

I assume that you are somewhat computer literate but have had little or no experience with Linux (or UNIX). You might be migrating from Microsoft operating systems to Red Hat Linux because of its networking and multiuser features. You might be looking to start a career as a computer technician or network administrator and find that spending a few dollars for an entire operating system and book is more economical than taking those technical classes offered on late-night television. Or you might just think a “free” operating system is cool.

In any case, after you peruse this book you should have a good idea of how to run applications, set up a small network, connect to the Internet, and configure a variety of server types (Web servers, print servers, file servers, and so on). This book represents a great first couple of steps toward your becoming someone who can set up a home network or a small office network and maintain a group of computers.

### This Book’s Learn-through-Tasks Approach

The best way to learn a computer system is to get your hands on it. To help you learn Red Hat Linux, this book takes a task-oriented approach. Where possible, I step you through the process of working with a feature, such as setting up a network or configuring your desktop.

When you are done with a task, you should have a good, basic setup of the feature that it covers. After that, I often provide pointers to further information on tweaking and tuning the feature.

Instead of assuming that you already know what cryptic topics such as troff, NFS, and TCP/IP are, I ease you into those features with headings such as “Publishing with Red Hat Linux,” “Setting up a File Server,” and “Connecting to the Internet.” Heck, if you already knew what all those things were and how to get them working, you wouldn’t need me, would you?

When many tools can be used to achieve the same results, I usually present one or two examples. In other words, I don’t describe six different Web browsers, twelve different text editors, and three different news servers. I tell you how to get one or two similar tools really working and then note the others that are available.
