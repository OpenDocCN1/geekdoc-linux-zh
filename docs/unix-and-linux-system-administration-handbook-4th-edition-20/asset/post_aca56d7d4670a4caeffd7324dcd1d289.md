
## Use banner pages only if you have to

Your system can usually use print header and trailer pages for each job that show the title of the job and the user who submitted it. These banner pages are sometimes useful for separating jobs on printers used by many different people, but in cases they're a waste of time, toner, and paper.

On BSD systems, suppress them by setting the Boolean printcap variable sh. On System V systems, don't have your interface script generate them.

With CUPS, you can globally disable banner pages in your GUI or by running Ipadmin, then turn them on for any individual jobs that might benefit from them:

```bash
$ lpr o-jobs-sheets gilly.ps
```

CUPS lets you turn on banners for individual users using Options. You can also create a printer instance that adds banner pages to jobs (see Printer instances on page 1036). CUPS also lets you create a custom banner page by copying an existing one from /usr/share/cups/banners and modifying it. Put the new page in your others with a new name.

## Fan your paper

Printers are supposed to pull one page at a time from the paper tray. Sometimes, blank pages stick together and your printer will try to feed two or more pages at a time. You can minimize the frequency of this problem by jamming banner paper before you load. Hold one side of the ream, bend the paper, and run your thumb the opposite edge as you would riff through a deck of cards. Low-tech, it's free, and it works.

Some inkjet paper cares which side is up. Your packaging should indicate the orientation.

## Provide recycling bins

All kinds of computer paper are recyclable. You can use the boxes that paper comes in recycling bins; the paper fits in them perfectly. Post a sign asking that no foreign material (such as staples, paper clips, or newspaper) be discarded there.

## Previews

Users often print a document, find a small error in the formatting, fix it, and reprint the job. This waste of paper and time can easily be avoided with software that lets users see, on-screen, what the printed output will look like.

Having previews is not enough; your users need to know how to use them. They're sometimes happy to learn. One of accounting records is to check for cases in which the same document has been reprinted repeatedly. It can point you to a user who doesn't know about previews.

Previewing is built into many modern WYSIWYG editors, browsers, and print-job aggregators. For other types of documents, your options vary. Tools such as Ghostview (gv) preview random PostScript and PDF documents. For roff, pipe the output of groff into Ghostview; for TeX output, try xdvi, kdvi, or Evince.

## Buy cheap printers

Printer hardware technology is mature. You don't need to spend a lot of money for good output and reliable mechanisms.

Don't splurge on an expensive "workgroup" printer just because you have a work-group. If you are only printing text, an inexpensive "personal" printer can produce good-quality output, nearly as fast and reliable, and weighs tens of pounds less. One-page-a-minute printer can serve five full-time writers. You may be better off buying five $150 printers for a group of 25 writers than one $750 printer.

Even if you stick to mainstream brands, no individual manufacturer is a universal-safe bet. We have had excellent experiences with HP for solid products, and HP has been very aggressive in supporting both Linux and CUPS. For so, some of HP's printers have been complete disasters. Look for reviews on the Internet before buying. Here, too, cheap is an advantage: a $150 mistake is easier to cover up than a $750 mistake.

## Keep extra toner cartridges on hand

Faded blank areas on a laser-printed page are hints that the printer is running out of toner. Buy replacement cartridges before you need them. In a pinch, move the cartridge from the printer and gently rock it to redistribute the remaining toner particles. You can often get another few hundred pages of a cartridge this way.

Streaks and spots probably mean you should clean your printer. Look on the printer to see if there is a "clean" cycle. If not, or the cleaning cycle doesn't help, read the manufacturer's cleaning instructions. Most toner cartridges include an imaging drum, so swapping toner cartridges to verify that the problem is really the printer and not the cartridge. None of these resolve the streaks, pay to have the printer serviced.

Printer manufacturers hate the use of generic toner cartridges, and they go to great lengths to prevent it. Many devices use "keyed" consumables whose identities are detected (either electronically or physically) by the printer. Even if two printers look identical, such as the Xerox Phaser 6120 and the Konica-Minolta Magicolor 2450, it does not necessarily mean that you can use the same cartridges in both.

Sometimes you do surgery to convert one vendor's cartridges to another printer, but it helps to know what you're doing. Usually, you just make a mess. If you spill toner, vacuum up as much of the material as possible and wipe the remainder with cold water. Contrary to common belief, laser toner is not toxic, but with all fine powders, you should not inhale the toner dust.

![](img/579efec8c67772f31ecf34844bbb71a2_1127_0.png)

When you replace a cartridge, save the box and baggie the new cartridge came in use when recycling the spent one. Find a company to take the old cartridge off your hands.

Keyed consumables spurred the growth of companies ("punch and pours") that refill cartridges for a fraction of the new-cartridge price. Cartridge recyclers are usually punch-and-pours, so you can recycle your old cartridges and get replacements at the same time.

Opinions on the quality and life span of recycled cartridges vary. One punch-and-pour we won't refill toner cartridges or sell manufactured ones because they believe the savings are less than the increased maintenance costs for the printers that use them.

## Pay attention to the cost per page

Most expensive printers are sold at close to their manufacturing cost. The manufacturers make their money on the consumables, which are disproportionately expensive. As of this writing, a quick check reveals that Amazon is selling for $80 laser printer that takes toner costly $65. You can buy a cheap printer for less than $50 at Wal-Mart, but it won't be long before you need to buy a set of replacement inkjet cartridges that cost more than the printer. You can feign outrage over this, but printer companies have to make their money on something. Cheaper cartridges would mean cheaper printers.

A good rule of thumb is that inkjet printers last as long as you don't print with them. Laser printers have a higher initial cost, but the consumables are cheaper and last. A full-color page from an inkjet printer costs 20–50 times as much as an analog print from a laser printer. It also requires special paper and prints more slowly. Ink cartridges dry quickly and frequently plug up or go bad. The inkjet runs when wet, so don't use inkjet to print a recipe book for use in the kitchen. On the other hand, you can now get photo prints from an inkjet that looks as good as prints from a photo lab. Color laser No, comparison. For low-volume, personal use—printing a web page or two a day, or printing a couple of rolls of film per month—a low-cost, general purpose inkjet is an excellent choice. Next time you go printer shopping, estimate how long you want to keep your printer, how much printing you do, and what kind of printing you need before you buy. Assess quantitatively the long-term cost per page for each candidate printer. Ask your local punch-and-pour where they remanufacture cartridges for the printer, and at what price.

- Keep in mind, though that many inexpensive printers come with "starter" cartridges that include less ink or toner than a standard replacement.
