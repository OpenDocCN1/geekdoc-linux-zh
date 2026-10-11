
- **scanimage**: This program, which I introduced earlier as a means to locate scanner devices, is actually a basic scanner program for Linux. You can use it to create a PNM graphics file from a scanner. For instance, typing `scanimage --device=muster /dev/scanner > image.pnm` creates the image.pnm graphics file from the mustek /dev/scanner device. Many scanner devices support device-specific parameters you can pass to scanimage. For instance, the pnm devices, which read from a file, require the `--filename=file.ext` parameter to tell the back end what file to read.

- **xscanimage**: This program provides an X-based interface to SANE, as shown in Figure 19.6. Each device’s interface contains somewhat different options.

![](img/860d0c38bd76c9ded976e9d1e179ef25_549_0.png)

Figure 19.6

GUI scanner utilities provide you with easy-to-use sliders and buttons to adjust scan brightness and other features.

- **The GIMP**: The GNU Image Manipulation Program (GIMP) is a powerful and popular Linux graphics program. The GIMP accepts plug-ins—small programs written by a variety of authors that extend the GIMP’s capabilities. SANE comes with a plug-in for the GIMP that enables the GIMP to acquire images directly from a scanner.
- **GOCR**: The GNU Optical Character Recognition (GOCR; see http://altmark.nat.uni-magdeburg.de/~jschulen/gocr/) is an early attempt at OCR software for Linux. This software takes a graphical input file and creates a textual output file. GOCR doesn’t actually accept input directly from a scanner; you must scan to a file and then feed the results through the program. I mention it here because OCR is one of the more interesting applications of scanners. Compared to OCR software for Windows, GOCR is primitive, but it might improve over time.

- **OCRShop**: This commercial package costs between $99 and $3,295, depending upon your scanner model and use (personal, nonprofit, or corporate). This program, unlike most Linux scanner applications, does *not* work through SANE, so its list of supported scanners doesn’t match that of SANE. It’s built on Caere’s (http://www.caere.com) OmniPage OCR technology. You can find out more from Vividata’s OCRShop Web page, http://www.vividata.com/ocrshop.html.

As Linux’s scanner support continues to mature, and as Linux grows in popularity, more SANE-enabled applications are likely to arrive on the scene. Check the main SANE Web page at http://www.mostang.com/sane/ for the latest information.

## Summary

As a general rule, flatbed scanners are the most flexible type of scanner available for most uses. These devices consume a great deal of desk space, however, so you might prefer a sheet-fed or hand scanner, particularly if you want a scanner to accompany you when you take a laptop computer on the road.

Linux support for scanners is variable. Linux works with most SCSI scanners, an increasing number of USB scanners, and a few parallel-port scanners. Linux support for scanners comes largely in the form of the SANE project, which provides a uniform programming interface for application developers.

## Printers

CHAPTER 20

### IN THIS CHAPTER

- **Types of Printer Hardware** 530
- **Choosing a Printer Interface** 537
- **Printer Languages** 541
- **Using Printers in Linux** 547

The “paperless office” was a vision of the 1970s and early 1980s. With the advent of personal computers on every office worker’s desk, people thought there would be a decreasing need for paper documents. Unfortunately for many trees, this vision is far from becoming reality, and will likely remain remote for years. The reason is simple: Computers—through printers—make it *easier* to produce paper documents than ever before.

Linux includes good support for printers. Linux’s printer support, unlike support for most other devices, doesn’t lie so much in the Linux kernel as it does in a separate program, known as *Ghostscript*. I describe Ghostscript later in this chapter. First, though, it’s necessary to understand more basic information about printer technology, such as the assorted methods used to print and the types of interfaces and printer languages available.

### Types of Printer Hardware

The goal of a printer is to place text or images on a sheet of paper. Over the years, manufacturers have developed quite a few technologies to accomplish this goal. Physical contact with an intervening inked ribbon, squirting ink, and photocopier-like technologies have all been common. Each of these technologies has its merits and its flaws. *If you’re in the market for a printer, one of the first decisions you should make is which of the many printing technologies you want to embrace.*

#### Laser Printers

Laser printers are the current favorite form of office printer. These printers work on principles similar to those of photocopiers. They also traditionally require a fair amount of computing power in the printer itself, although some recent models change this fact.

##### Basic Laser Printer Technology

Laser printing centers on the printer’s *drum*, which is a light-sensitive cylinder. A laser printer imparts an electrostatic charge on the drum. When exposed to light, the drum’s electrostatic charge changes. A laser and mirror assembly “paints” an image of the document to be printed on the drum, which simultaneously rotates. As the drum rotates, it’s brought near a reservoir of *toner*, which is a static-sensitive plastic powder. The toner sticks to the drum in the areas that have been struck by the laser’s light. Further rotation of the drum brings it into contact with paper, which has also been charged, so the toner is drawn from the drum onto the paper. The paper is then heated in a *fuser* assembly to a high-enough temperature to melt the toner, which quickly cools and sticks to the paper. Additional components then return the drum surface to its original state, and the process begins again. Figure 20.1 illustrates this process.

![](img/860d0c38bd76c9ded976e9d1e179ef25_553_0.png)

Figure 20.1

*A laser printer’s inards use a number of precision components operating in concert to produce a legible image.*

A variant on the laser printer is the *LED printer*, which uses a bank of *light emitting diodes* (LEDs) in place of the laser and mirror shown in Figure 20.1. Aside from anything having to do with lasers, everything I write in this chapter about laser printers applies to LED printers, as well. In fact, many people refer to LED printers as *laser printers*, despite the fact that there’s no laser in an LED printer. The term *page printer* is sometimes used to refer to both types of printer.

Most laser printers include the drum assembly in a sealed package along with the toner. Because the drum eventually wears out, this arrangement allows for easy replacement of the drum when the toner runs out. Other models have separate drum units and toner supplies. With these, the drum is typically designed to last longer, but it’s more expensive than the drum/toner units of other models. When you compute the estimated operating costs of a laser printer, be sure to consider both the toner and (if it’s separate) drum cartridges.

> **CAUTION**
>
> Laser printer toner cartridges are not usually interchangeable. Also, some firms offer recycled toner cartridges or toner cartridge refill kits. The more reputable firms rebuild their toner cartridges, but some companies do a poor job when refilling toner cartridges with new toner. Refill kits are likely to be of poor quality. I therefore suggest you proceed with caution when using recycled cartridges. Be sure to find out how much effort the firm employs in checking and, if necessary, replacing worn components.

The process of printing a page in a laser printer is very timing-sensitive. If the mechanism stops mid-page, the part of the page in the fuser assembly can become scorched, and the
