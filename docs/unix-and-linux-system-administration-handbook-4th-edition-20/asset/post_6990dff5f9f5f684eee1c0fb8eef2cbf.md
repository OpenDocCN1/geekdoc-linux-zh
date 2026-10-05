
# UNIX AND LINUX® SYSTEM ADMINISTRATION HANDBOOK
FOURTH EDITION

EVI NEMETH • GARTH SNYDER • TRENT R. HEIN • BEN WHALEY with Terry Morreale, Ned McClain, Ron Jachim, David Schweikert, and Tobi Oetiker

# UNIX® AND LINUX® SYSTEM ADMINISTRATION HANDBOOK
FOURTH EDITION

Evi Nemeth
Garth Snyder
Trent R. Hein
Ben Whaley

with Terry Morreale, Ned McClain,
Ron Jachim, David Schweikert, and Tobi Oetiker

![](img/579efec8c67772f31ecf34844bbb71a2_3_0.png)

PRENTICE HALL
Upper Saddle River, NJ • Boston • Indianapolis • San Francisco
New York • Toronto • Montreal • London • Munich • Paris • Madrid
Capetown • Sydney • Tokyo • Singapore • Mexico City

Many of the designations used by manufacturers and sellers to distinguish their products are claimed as trademarks. Where those designations appear in this book, and the publisher was aware of a trademark claim, the designations have been printed with initial capital letters or in all capitals.

Red Hat Enterprise Linux and the Red SHADOWMAN are registered trademarks of Red Hat Inc., and such trademarks are used with permission.

Ubuntu is a registered trademark of Canonical Limited, and is used with permission.

SUSE and openSUSE are registered trademarks of Novell Inc. in the United States and other countries.

Oracle Solaris and OpenSolaris are registered trademarks of Oracle and affiliates. All rights reserved.

HP-UX is a registered trademark of Hewlett-Packard Company. (HP-UX*)

AIX is a trademark of IBM Corp., registered in the US and other countries.

The authors and publisher have taken care in the preparation of this book, but make no expressed or implied warranty of any kind and assume no responsibility for errors or omissions. Liability is assumed for incidental or consequential damages in connection with or out of the use of the information or programs contained herein.

The publisher offers excellent discounts on this book ordered in bulk purchases or special sales, which may include electronic versions and/or custom content particular to your business, training goals, marketing, and branding interests. For more information, please contact:

U.S. Corporate and Government Sales
(800) 382-3419
corpsales@pearsontechnology.com

For sales outside the United States, please contact International Sales (international@pearson.com).

Visit us on the Web: itform.com/ph handbook.

Library of Congress Cataloging-in-Publication Data

UNIX and Linux system administration handbook / Evi Nemeth ... [et al.].—4th ed.

+ p. cm.
4th ed of: Unix system administration handbook, 3rd ed., 2001.
Includes index.
ISBN 978-0-13-148005-6 (pbk.)
1. Operating systems (Computers) 2. UNIX (Computer file) 3. Linux.
1. Nemeth, Evi. II system administration handbook.
QA76.76.O63N45 2010
005.43–dc22

Copyright © 2011 Pearson Education, Inc.
All rights reserved. The publication in the United States of America. This publication is protected by copyright, and permission must be obtained from the publisher prior to any prohibited reproduction, storage in a retrieval system, or transmission in any form or by any means, mechanical, photocopying, recording, or likewise. For information regarding permissions, write to:

Pearson Education, Inc.
Rights and Contracts Department
501 Boyston Street, Suite 900
Boston, MA 02116
Fax: (617) 671-3447

ISBN-13: 978-0-13-148005-6
ISBN-10: 0-13-148005-5

Text printed in the United States on recycled paper at Edwards Brothers in Ann Arbor, Michigan.
First printing, June 2010

2010018773

# Table of Contents

- FOREWORD ................................................................................ xii
- PREFACE ................................................................................ xiv
- ACKNOWLEDGMENTS ...................................................... xlvi

## SECTION ONE: BASIC ADMINISTRATION

### CHAPTER 1 WHERE TO START 3
- Essential duties of the system administrator ................................ 4
- Account provisioning. ................................................................. 4
- Adding and removing hardware. ................................................... 4
- Performing backups ..................................................................... 5
- Installing and upgrading software ........................................ 5
- Monitoring the system. ................................................................... 5
- Troubleshooting ............................................................................ 5
- Maintaining local documentation ................................................ 5
- Vigilantly monitoring security ...................................................... 6
- Fire fighting ................................................................................. 6
- Suggested background ......................................................................... 6
- Friction between UNIX and Linux ........................................................ 7
- Linux distributions ................................................................... 9
- Example systems used in this book .................................................. 10
- Example Linux distributions ...................................................... 11
- Example UNIX distributions ....................................................... 12
- System-specific administration tools ..................................................................................... 13
Notation and typographical conventions ................................................................................................ 13
Units ................................................................................. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 14
Man pages and other on-line documentation .......................................................................................... 16
  Organization of the man pages ................................................................................................................. . . . . 16
  man: read man pages ................................................................................................................................. . . . . . . . . . . . 17
  Storage of man pages ................................................................................................................................. . . . . 17
  GNU Texinfo. ................................................................................................................................................... 18
Other authoritative documentation. ....................................................................................................... 18
  System-specific guides ................................................................................................................................... 18
  Package-specific documentation .......................................................................................................................... 19
  Books ........................................................................................................................................................................... 19
  RFCs and other Internet documents ................................................................................................................... 20
  The Linux Documentation Project ................................................................................................................ 20
Other sources of information ....................................................................................................................... 20
Ways to find and install software ..................................................................................................................... 21
  Determining whether software has already been installed. ............................................................................ 22
  Adding new software ................................................................................................................................................... 23
  Building software from source code ................................................................................................................... 25
System administration under duress ................................................................................................ 26
Recommended reading ....................................................................................................................................... 27
  System administration ...................................................................................................................................... 27
  Essential tools .............................................................................................................................................................. 27
Exercises. ........................................................................................................................................................ 28

# CHAPTER 2 SCRIPTING AND THE SHELL 29
- Shell basics. ...................................................................................................................................... 30
  Command editing. .............................................................................................................................................. 30
  Pipes and redirection ...................................................................................................................................... 31
  Variables and quoting ................................................................................................................................ 32
  Common filter commands ............................................................................................................................... 33
  cut: separate lines into fields ...................................................................................................................... 34
  sort: sort lines .......................................................................................................................................................... 34
  uniq: print unique lines ................................................................................................................................... 35
  wc: count lines, words, and characters ................................................................................................ 35
  tee: copy input to two places ................................................................................................................ 35
  head and tail: read the beginning or end of a file ................................................................................ 36
  grep: search text ............................................................................................................................................ 36
