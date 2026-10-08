
## The Linux Companion for System Administrators
second edition

Jochen Hein

## The LINUX Companion for System Administrators

## The LINUX Companion for System Administrators
Jochen Hein

ADDISON-WILLEY
im imprint of Pearson Education
Harlow, England • London • New York • Reading, Massachusetts • San Francisco • Toronto • Don Mills, Ontario • Sydney • Tokyo • Singapore • Hong Kong • Seoul • Taipei • Cape Town • Madrid • Mexico City • Amsterdam • Munich • Paris • Milan

## PEARSON EDUCATION LIMITED

Head Office:
London Office:
Edinburgh Gate
128 Long Acre
Harlow
London WC2E 9AN
CM20 2FE
Tel: +44(0)207447 2000
Tel: +44(0)1279 623623
Fax: +44(0)207240 5771
Fax: +44(0)1279 431059
Websites: www.it-minds.com
www.aw.com/cseng/

This edition first published in Great Britain 2001.

© Pearson Education Ltd 2001

The right of Jochen Hein to be identified as author of this Work has been asserted by him in accordance with the Copyright, Designs and Patents Act 1988.

ISBN 0-201-67525-0

## British Library Cataloging-in-Publication Data

A catalogue for this book is available from the British Library

## Library of Congress Cataloging-in-Publication Data

Applied for.

All rights reserved. No part of this publication may be reproduced, stored in a retrieval system, or transmitted in any form or by any means, electronic, mechanical, photocopying, recording or otherwise, without the prior written permission of the publisher or a licence permitting restricted copying in the United Kingdom issued by the Copyright Licensing Agency Ltd, 90 Tottenham Court Road, London W1P 0LPP.

The programs in this book have been included for their instructional value. They have been tested with care but are not guaranteed for any particular purpose. The publisher does not offer any warranties or representations nor does it accept any liabilities with respect to the programs.

Many of the designations used by manufacturers and sellers to distinguish their products are claimed as trademarks. Pearson Education Limited has made every attempt to supply trademark information about manufacturers and their products mentioned in this book. A list of the trademark designations and their owners appear on page xvi.

+ 10 9 8 7 6 5 4 3 2 1

Translated and typeset by Cybernetics, Sheffield, United Kingdom
Printed and bound in Great Britain by Biddles Ltd, Guildford.

The publishers' policy is to use paper manufactured from sustainable forest.

## Preface

We are not developing a system to take over the OS market, we are just having a good time.

Michael L. Kaufman in Comp.os.minux about LINUX development

LINUX is a UNIX-like operating system. Thus, a LINUX system has all the flexibility, but also all the complexity, of UNIX. This book is meant as a contribution to help users to get grips with this complexity and make efficient use of the flexibility.

LINUX is a free operating system. This applies not only to the kernel, but also to almost all the programs. Free, for the GNU General Public License (GPL), means that the source code is freely available. It does not refer to the sometimes free-of-charge distribution of LINUX via mailboxes or ftp servers.

In the freeware scarce, there are basically four different kinds of license:

- the BSD or X copyright, which also allows the code to be used in commercial and proprietary systems;
- the GPL, which requires that the programs or improved versions derived from them continue to be free;
- programs whose commercial use or distribution is prohibited;
- programs that are not subject to any copyright, the so-called public domain programs.

These liberal licensing conditions made LINUX what it is today. A decisive role was played by the availability of GNU programs, which had already made the utilities of a UNIX system freely available. Another important issue was the X Window system port, which is today available as XFree86 for LINUX (and a series of other UNIX systems).

## VI PREFACE

Free software is better software, because it gives the user the chance to adapt, improve, and understand the programs, or simply correct errors. This opportunity is denied to users of proprietary software, who are at the mercy of software distributors, for better or for worse. Apart from the possibility of gaining complete insight into the system, this is the most striking argument in favour of LINUX or any other free system, such as NetBSD, FreeBSD, OpenBSD, or Hurd. A further advantage for the user is that various suppliers can provide support for the system.

Besides the programs themselves, the corresponding documentation is also freely available. The LINUX Documentation Project has made it business to write both HowTo and complete manuals. Some of these books are also available in bookstores. These are also projects to translate the HowTos into several foreign languages.

However, you do not have to be a programmer to employ Linux efficiently. If errors occur, they are often found and corrected by programmers within a few hours or days. Especially if you have installed a 'stable' distribution of LINUX, the system will run steadily and reliably from the very first moment. Installation of new programs or an update to a new version is usually limited to the execution of a few commands.

This book has been written almost entirely with free software. Emacs and Te were used as editors, together with LaTeX for the typesetting of texts. The stability and speed of LINUX together have played a major role in the success. This book is dedicated to all programmers (and users), without whom today's multitude of software would not exist.

## Typographical conventions

Following the tradition of most computer books, I would like to dedicate a section to the presentation of typographical conventions. These are intended to improve readability and avoid repeated explanations of basic features.

- Computer output is set in a special font (Computer Display).
- User input is set in the same font, but additionally highlighted using bold characters.

## PREFACE VII

- Variable input that has to be replaced as appropriate by the user is shown in italics.
- To differentiate between various shells and privileged and non-privileged users, we use different prompts:

- stands for the system administrator, who uses bash.
- stands for a user with tsh.
- stands for a user with bash.

Let us look at an example produced by a `tsh` user. The user is used in this book only in places where it is mandatory. The separation between user and system administrator is one of the fundamental concepts of UNIX and serves the security of user and system data and the stability of the system.

```
(Linux):~ echo 'This is an input' | sed s/in/out/
This is an output
```

Additional special formatting is used for shell or environment variables (VARIABLE). Names of programs and commands are set in display font (program), files are specified including the path (/path/file). Listings or excerpts from configuration files are set in display font (Computer Display), and so are names of computers. The use of key combinations is represented in the following form:

- for the A key, Del for the Del key
- Ctrl-C for simultaneous pressing of Ctrl and C
- Esc-X for the key sequence Esc followed by X

## Access paths for files

For every program package included, you will find an indication of where to find the programs or additional information. Possibly you may want to install an updated version of some software at a later stage; for this reason, a source where the software can be obtained is indicated with every program described.
