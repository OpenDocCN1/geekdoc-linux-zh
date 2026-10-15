

# UNIX 和 Linux 系统管理手册

第四版

![](img/14d78e3cecac4581d37024baf1e94cca_0_0.png)

EVI NEMETH · GARTH SNYDER · TRENT R. HEIN · BEN WHALEY

with Terry Morreale, Ned McClain, Ron Jachim, David Schweikert, and Tobi Oetiker

# UNIX® AND LINUX® SYSTEM ADMINISTRATION HANDBOOK
FOURTH EDITION

# UNIX AND LINUX SYSTEM ADMINISTRATION HANDBOOK

FOURTH EDITION

Evi Nemeth
Garth Snyder
Trent R. Hein
Ben Whaley

with Terry Morreale, Ned McClain,
Ron Jachim, David Schweikert, and Tobi Oetiker

![](img/14d78e3cecac4581d37024baf1e94cca_3_0.png)

Upper Saddle River, NJ • Boston • Indianapolis • San Francisco
New York • Toronto • Montreal • London • Munich • Paris • Madrid
Capetown • Sydney • Tokyo • Singapore • Mexico City

Many of the designations used by manufacturers and sellers to distinguish their products are claimed as trademarks. Where those designations appear in this book, and the publisher was aware of a trademark claim, the designations have been printed with initial capital letters or in all capitals.

Red Hat Enterprise Linux and the Red Hat SHADOWMAN logo are registered trademarks of Red Hat Inc., and such trademarks are used with permission.

Ubuntu is a registered trademark of Canonical Limited, and is used with permission.

SUSE and openSUSE are registered trademarks of Novell Inc. in the United States and other countries.

Oracle Solaris and OpenSolaris are registered trademarks of Oracle and/or its affiliates. All rights reserved.

HP-UX is a registered trademark of Hewlett-Packard Company. (HP-UX®)

AIX is a trademark of IBM Corp., registered in the U.S. and other countries.

The authors and publisher have taken care in the preparation of this book, but make no expressed or implied warranty of any kind and assume no responsibility for errors or omissions. No liability is assumed for incidental or consequential damages in connection with or arising out of the use of the information or programs contained herein.

The publisher offers excellent discounts on this book when ordered in quantity for bulk purchases or special sales, which may include electronic versions and/or custom covers and content particular to your business, training goals, marketing focus, and branding interests. For more information, please contact:

U.S. Corporate and Government Sales
(800) 382-3419
corpsales@pearsontechgroup.com

For sales outside the United States, please contact International Sales (international@pearson.com).

Visit us on the Web: informit.com/ph

Library of Congress Cataloging-in-Publication Data
UNIX and Linux system administration handbook / Evi Nemeth ... [et al.].
—4th ed.
p. cm.
Rev. ed. of: Unix system administration handbook, 3rd ed., 2001.
Includes index.
ISBN 978-0-13-148005-6 (pbk. : alk. paper)
1. Operating systems (Computers) 2. UNIX (Computer file) 3. Linux.
I. Nemeth, Evi. II. Unix system administration handbook.
QA76.76.O63N45 2010
005.4'32—dc22
2010018773

Copyright © 2011 Pearson Education, Inc.

All rights reserved. Printed in the United States of America. This publication is protected by copyright, and permission must be obtained from the publisher prior to any prohibited reproduction, storage in a retrieval system, or transmission in any form or by any means, electronic, mechanical, photocopying, recording, or likewise. For information regarding permissions, write to:

Pearson Education, Inc.
Rights and Contracts Department
501 Boylston Street, Suite 900
Boston, MA 02116
Fax: (617) 671-3447

ISBN-13: 978-0-13-148005-6
ISBN-10: 0-13-148005-7

Text printed in the United States on recycled paper at Edwards Brothers in Ann Arbor, Michigan.

First printing, June 2010

# 目录

FOREWORD ........................................................................ xlii
PREFACE .......................................................................... xliv
ACKNOWLEDGMENTS ................................................................. xlvi

## 第一部分：基础管理

## 第 1 章 从哪里开始 ........................................................ 3

系统管理员的基本职责 ........................................ 4

- 账户配置 .............................................................. 4
- 添加和移除硬件 ......................................................... 4
- 执行备份 .................................................................... 5
- 安装和升级软件 ....................................................... 5
- 监控系统 ................................................................. 5
- 故障排除 ........................................................................ 5
- 维护本地文档 ........................................................ 5
- 警惕监控安全 .......................................................... 6
- 救火 ........................................................................... 6

建议的备份 ..................................................................... 6
UNIX 与 Linux 之间的摩擦 ......................................................... 7
Linux 发行版 ..................................................................... 9
本书中使用的示例系统 ...................................................... 10

- 示例 Linux 发行版 .......................................................... 11
- 示例 UNIX 发行版 ............................................................ 12

