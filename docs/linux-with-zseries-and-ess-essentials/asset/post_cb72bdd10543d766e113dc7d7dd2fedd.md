
## Linux with zSeries and ESS: Essentials

- Enterprise-class solutions with Linux and IBM TotalStorage
- Focus on zSeries and ESS
- FCP support for Linux on zSeries

![](img/da33d6b6aa12b73deb3c350a0a89d424_0_0.png)

Bertrand Dufresne
Don Skilton
Jonathan Wright

## Redbooks

![](img/da33d6b6aa12b73deb3c350a0a89d424_2_0.png)

International Technical Support Organization

## Linux with zSeries and ESS: Essentials

September 2003

**Note:** Before using this information and the product it supports, read the information in “Notices” on page ix.

## Contents

Figures ........................................................... v
Tables ........................................................... vii
Notices ........................................................... ix
Trademarks ........................................................ x

Preface ........................................................... xi
The team that wrote this redbook. .................................... xi
Become a published author ............................................ xii
Comments welcome. ................................................... xii

## Chapter 1. Introduction to Linux ..................................... 1
### 1.1 The foundation for Linux ......................................... 2
### 1.2 The GNU General Public License ................................... 2
### 1.3 Open source ...................................................... 3
### 1.4 Linux: The operating system ...................................... 3
### 1.5 Where Linux fits in .............................................. 4
### 1.5.1 Working with other operating systems ........................... 4
### 1.5.2 Infrastructure ................................................ 5
### 1.6 Linux distributions .............................................. 5
### 1.6.1 Red Hat Enterprise Linux ...................................... 5
### 1.6.2 SuSE Linux Enterprise Edition .................................. 6
### 1.6.3 UnitedLinux ................................................... 6

## Chapter 2. IBM and Linux ............................................. 9
### 2.1 IBM's commitment to Linux ....................................... 10
### 2.1.1 The IBM Linux Technology Centers .............................. 11
### 2.2 Linux services and application solutions ......................... 11
### 2.2.1 IBM Services .................................................. 12
### 2.2.2 IBM Global Services ........................................... 12
### 2.2.3 IBM Support Line .............................................. 12
### 2.2.4 Linux consultancy ............................................. 13
### 2.3 IBM services and software ....................................... 14
### 2.3.1 WebSphere ..................................................... 14
### 2.3.2 DB2 for Linux ................................................. 15
### 2.3.3 Tivoli ........................................................ 15
### 2.3.4 Lotus ......................................................... 18
### 2.4 Platform services ............................................... 18
### 2.4.1 zSeries services .............................................. 19
### 2.4.2 iSeries services .............................................. 19
### 2.4.3 pSeries services .............................................. 20
### 2.4.4 xSeries services .............................................. 20
### 2.4.5 Consolidated platform matrix .................................. 21

## Chapter 3. zSeries and Linux ......................................... 23
### 3.1 Introduction .................................................... 24
### 3.1.1 Ways to run Linux on zSeries .................................. 24
### 3.1.2 S/390 and zSeries architecture ................................ 25
### 3.1.3 Further information ................................................ 26
### 3.2 Background to z/VM ................................................ 27
### 3.2.1 Virtual networking with z/VM ........................................ 28
### 3.2.2 Systems management functions built-in to z/VM ...................... 29
### 3.3 Consolidation and scalability ........................................ 29
### 3.3.1 Scalability ................................................ 29
### 3.3.2 Consolidation ................................................ 29
### 3.3.3 Some examples and further information ............................ 31
### 3.4 Linux application solutions ........................................ 31

## Chapter 4. IBM TotalStorage and ESS ........................................ 35
### 4.1 IBM TotalStorage ................................................ 36
### 4.1.1 Value proposition .............................................. 36
### 4.2 IBM TotalStorage Proven™ ........................................... 37
### 4.3 Enterprise Storage Server .......................................... 38
### 4.3.1 ESS overview ................................................ 38
### 4.3.2 ESS features and benefits ....................................... 39
### 4.3.3 ESS Specialist ................................................ 44

## Chapter 5. FCP for zSeries with Linux ...................................... 47
### 5.1 zSeries and FCP .................................................. 48
### 5.1.1 zSeries specific storage attachments .............................. 48
### 5.1.2 Distributed storage attachments .................................. 49
### 5.1.3 zSeries-specific versus distributed storage controllers ........... 50
### 5.2 Connecting ESS to Linux on zSeries using FCP ....................... 52
### 5.2.1 Hardware and software requirements ............................... 53
### 5.2.2 An implementation overview ...................................... 53

## Chapter 6. ESS Copy Services and Linux .................................... 61
### 6.1 Introduction .................................................... 62
### 6.2 Peer-to-Peer Remote Copy (PPRC) .................................... 63
### 6.3 PPRC Extended Distance (PPRC-XD) ................................... 65
### 6.4 FlashCopy ....................................................... 68
### 6.5 ESS Copy Services Web User Interface ............................... 71
### 6.6 Copy Services command line interface ............................... 76
### 6.7 ESS Copy Services available with Linux on zSeries .................. 77

Related publications ................................................... 79
IBM Redbooks ........................................................ 79
Other publications ................................................... 79
Online resources ..................................................... 79
How to get IBM Redbooks .............................................. 80
Help from IBM ........................................................ 80

Index ................................................................ 81

## Figures

3-1 IBM eServer zSeries ........................................ 24
3-2 Running Linux on zSeries in an LPAR or as a z/VM guest ............... 25
3-3 The relationship between IFLs and LPARs .............................. 26
3-4 Configuration of CPs for a zSeries running z/OS and Linux under z/VM. ........ 26
3-5 z/VM virtualization .............................................. 28
3-6 Server farm in a box............................................. 30
3-7 Horizontal server growth ........................................ 30
3-8 Samba file/print scenario - distributed solution .................... 32
3-9 Samba file/print scenario - zSeries solution........................ 33
4-1 IBM's Seascape® architecture - ESS Model 800 ........................ 38
4-2 ESS Model 800 major components ................................... 39
4-3 IBM TotalStorage Enterprise Storage Server for storage consolidation ...... 40
4-4 Enterprise Storage Server Model 800 ............................... 41
4-5 Disaster recovery and availability ............................... 42
4-6 Storage area network (SAN) ...................................... 44
4-7 ESS welcome screen.............................................. 45
5-1 Typical zSeries storage attachment concept......................... 48
5-2 SCSI addressing ................................................ 50
5-3 World Wide Names ............................................... 50
5-4 DASD addressing scheme......................................... 51
5-5 DASD access translations FICON vs. FCP ............................ 52
5-6 Storage Allocation panel ....................................... 54
5-7 Open Systems Storage panel ..................................... 54
5-8 Modify Host Systems panel - add the Linux on zSeries host........ 55
5-9 Configure Host Adapter ports panel.............................. 56
5-10 Fixed Block Storage panel..................................... 57
5-11 Add volumes (panel 1 of 2) .................................... 58
5-12 Add volumes (panel 2 of 2) .................................... 58
6-1 ESS Copy Services for zSeries .................................. 62
6-2 Synchronous volume copy PPRC ................................... 63
6-3 PPRC volume states - synchronous mode of operation .............. 65
6-4 PPRC-XD operation.............................................. 66
6-5 Duplex-pending XD volume state ................................ 67
6-6 PPRC-XD Basic operation....................................... 68
6-7 FlashCopy point-in-time copy .................................. 70
6-8 Incremental FlashCopy ........................................ 71
6-9 ESS Welcome screen ............................................ 72
6-10 Main menu ESS Copy Services Web User Interface.................. 72
6-11 Volumes panel................................................ 73
6-12 Logical Subsystems panel...................................... 74
6-13 Paths entry panel............................................. 75
6-14 Tasks panel .................................................. 76
