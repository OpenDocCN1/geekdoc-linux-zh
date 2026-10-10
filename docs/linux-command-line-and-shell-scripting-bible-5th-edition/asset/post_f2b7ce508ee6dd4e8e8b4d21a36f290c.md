
# COMPANION WEBSITE

**WRITTEN BY**

RICHARD BLUM
CHRISTINE BRESNAHAN

FIFTH EDITION

## Linux® Command Line
and Shell Scripting

# BIBLE

THE COMPREHENSIVE TUTORIAL RESOURCE

- EXPLORE THE LATEST TOOLS AND FEATURES
- MASTER INSIDE TRICKS AND BEST PRACTICES
- DISCOVER WHAT YOU NEED, WHEN YOU NEED IT

![](img/0798d50a0e5dbf1265fbda3832b3e015_0_0.png)

# Linux® Command Line and Shell Scripting

# BIBLE

# Linux Command Line and Shell Scripting

# BIBLE

THE COMPREHENSIVE TUTORIAL RESOURCE

Richard Blum
Christine Bresnahan

Fifth Edition

![](img/0798d50a0e5dbf1265fbda3832b3e015_4_0.png)

Copyright © 2026 by John Wiley & Sons, Inc. All rights reserved, including rights for text and data mining and training of artificial intelligence technologies or similar technologies.

Published by John Wiley & Sons, Inc., Hoboken, New Jersey.

No part of this publication may be reproduced, stored in a retrieval system, or transmitted in any form or by any means, electronic, mechanical, photocopying, recording, scanning, or otherwise, except as permitted under Section 107 or 108 of the 1976 United States Copyright Act, without either the prior written permission of the Publisher, or authorization through payment of the appropriate per-copy fee to the Copyright Clearance Center, Inc., 222 Rosewood Drive, Danvers, MA 01923, (978) 750-8400, fax (978) 750-4470, or on the web at www.copyright.com. Requests to the Publisher for permission should be addressed to the Permissions Department, John Wiley & Sons, Inc., 111 River Street, Hoboken, NJ 07030, (201) 748-6011, fax (201) 748-6008, or online at http://www.wiley.com/go/permission.

The manufacturer's authorized representative according to the EU General Product Safety Regulation is Wiley-VCH GmbH, Boschstr. 12, 69469 Weinheim, Germany, e-mail: Product_Safety@wiley.com.

Trademarks: Wiley and the Wiley logo are trademarks or registered trademarks of John Wiley & Sons, Inc. and/or its affiliates in the United States and other countries and may not be used without written permission. All other trademarks are the property of their respective owners. John Wiley & Sons, Inc. is not associated with any product or vendor mentioned in this book.

Limit of Liability/Disclaimer of Warranty: While the publisher and the authors have used their best efforts in preparing this work, including a review of the content of the work, neither the publisher nor the authors make any representations or warranties with respect to the accuracy or completeness of the contents of this work and specifically disclaim all warranties, including without limitation any implied warranties of merchantability or fitness for a particular purpose. Certain AI systems have been used in the creation of this work. No warranty may be created or extended by sales representatives, written sales materials or promotional statements for this work. The fact that an organization, website, or product is referred to in this work as a citation and/or potential source of further information does not mean that the publisher and authors endorse the information or services the organization, website, or product may provide or recommendations it may make. This work is sold with the understanding that the publisher is not engaged in rendering professional services. The advice and strategies contained herein may not be suitable for your situation. You should consult with a specialist where appropriate. Further, readers should be aware that websites listed in this work may have changed or disappeared between when this work was written and when it is read. Neither the publisher nor authors shall be liable for any loss of profit or any other commercial damages, including but not limited to special, incidental, consequential, or other damages.

For general information on our other products and services or for technical support, please contact our Customer Care Department within the United States at (800) 762-2974, outside the United States at (317) 572-3993 or fax (317) 572-4002.

Wiley also publishes its books in a variety of electronic formats. Some content that appears in print may not be available in electronic formats. For more information about Wiley products, visit our web site at www.wiley.com.

> Library of Congress Cataloging-in-Publication Data has been applied for.

- Print ISBN: 9781394364947
- PDF ISBN: 9781394364961
- EPUB ISBN: 9781394364954
- OBOOK ISBN: 9781394406364

Cover Design: Wiley

Cover Image: © aleksandarvelasevic/Getty Images

> To the Lord God Almighty, “in whom
> are hidden all the treasures of
> wisdom and knowledge.”
> —Colossians 2:3

## About the Authors

Richard Blum has worked in the IT industry for more than 35 years as both a systems and a network administrator. During that time, he's had the opportunity to work with lots of different computer products, including Windows, NetWare, Cisco, Avaya, different flavors of UNIX, and of course, Linux. Over the years he's also volunteered for several nonprofit organizations to help support small networks that had little financial support. Rich is the author of many Linux-based books for total Linux geeks and teaches online courses in Linux and web programming. When he's not busy being a computer nerd, Rich enjoys playing piano and bass guitar and spending time with his wife, Barbara, and their two daughters, Katie Jane and Jessica.

Christine Bresnahan started working with computers more than 30 years ago in the IT industry as a systems administrator. Christine is an adjunct professor at Ivy Tech Community College, where she teaches Linux certification and Python programming classes. She also writes books and produces instructional resources for the classroom. During her downtime, Christine enjoys spending time with her husband and family, hiking, and gardening.

## About the Technical Editor

**Daniel Wilson** has worked as an IT professional for over 38 years. His background ranges from software development, *NIX Engineer and Oracle DBA, consulting, security and as an author/co-author for several books on UNIX (Linux, Solaris, and HP-UX) and the Oracle database. He currently works as a Cloud Information System Security Officer (CISSO).

## Acknowledgments

First, all glory and praise go to God, who through His Son, Jesus Christ, makes all things possible and gives us the gift of eternal life.

Many thanks go to the fantastic team of people at John Wiley & Sons for their outstanding work on this project. Thanks to Kenyon Brown, the acquisitions editor, for offering us the opportunity to work on this book. Also thanks to Christine O'Connor, the managing editor, and Karen Weller, the project manager, for keeping things on track and making the book more presentable. The technical editor, Dan Wilson, did an amazing job of double-checking all of the work in this book, in addition to making suggestions to improve the content. Thanks Dan!

We would also like to thank Carole Jelen at Watterside Productions, Inc., for arranging this opportunity for us, and for helping us out in our writing careers.

Christine would like to thank her husband, Timothy, for his encouragement, patience, and willingness to listen, even when he has no idea what she is talking about. Rich would like to thank his wife, Barbara, for the life-sustaining baked goods she readily prepared to help him keep up his energy while writing!

## Contents at a Glance

Introduction ............................. xxii

- **Part I: The Linux Command Line** ... 1
  - Chapter 1: Starting with Linux Shells ... 3
  - Chapter 2: Getting to the Shell ... 17
  - Chapter 3: Basic Bash Shell Commands ... 37
  - Chapter 4: More Bash Shell Commands ... 69
  - Chapter 5: Understanding the Shell ... 93
  - Chapter 6: Using Linux Environment Variables ... 113
  - Chapter 7: Understanding Linux File Permissions ... 137
  - Chapter 8: Managing Filesystems ... 161
  - Chapter 9: Installing Software ... 181
  - Chapter 10: Working with Editors ... 201

- **Part II: Shell Scripting Basics** ... 229
  - Chapter 11: Basic Script Building ... 231
  - Chapter 12: Using Structured Commands ... 257
  - Chapter 13: More Structured Commands ... 291
  - Chapter 14: Handling User Input ... 319
  - Chapter 15: Presenting Data ... 347
  - Chapter 16: Script Control ... 369

- **Part III: Advanced Shell Scripting** ... 397
  - Chapter 17: Creating Functions ... 399
  - Chapter 18: Writing Scripts for Graphical Desktops ... 421
  - Chapter 19: Introducing sed and gawk ... 449
  - Chapter 20: Regular Expressions ... 477
  - Chapter 21: Advanced sed ... 497
  - Chapter 22: Advanced gawk ... 527
