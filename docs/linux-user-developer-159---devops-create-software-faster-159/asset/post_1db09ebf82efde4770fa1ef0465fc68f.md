
The number of stars is adjusted depending on the display resolution

## Full code listing

![](img/0fc17bd4c29dc437e3ac28a53f7559db_76_0.png)

## 10 Place the player

Time to work out where we're drawing the player and adjust the viewpoint. The player position is calculated twice in different positions and averaged to match the polygon and parallax effects. The position of a point on a circle is calculated:

```
x = cos( angle ) * radius
y = sin( angle ) * radius
```

Sin and cos have a centre at zero so we need to add the screen centre point to the player's X and Y. The player centre is calculated from the radius multiplied by the cosine of the player angle plus the screen centre.

## 11 Fix a speed

The `moveCount` and `moveDelay` variables are used to fix the player's movement speed around the level regardless of how many sections there are.

The next section checks to see which quarter of the screen the player is in and moves the centre accordingly. The playing field is moved by a few pixels each frame until limited by:

```
if centerX < ( gwidth / 2 ) + ( gwidth / 20 )
```

Finally, the player's position is calculated and drawn using the `polypot` command. The angle is fixed so the player faces the centre and the size is scaled against the display resolution.

## 12 Build a polygon

The `polystart` command allows a polygon to be built up from a series of lines and automatically filled in.

Rather than work out the automatic sums within every plot in the `polystart` statement, we have calculated them beforehand with c = cos( pAngle + 90 ) and s = sin( pAngle + 90 ) and u is the scale of the ship against the display resolution.

## 13 Polygon equation

Each X point on the polygon is based on (scale * line length) multiplied by cos( playerAngle + 90 ), minus ( scale * line length) multiplied by sin( playerAngle + 90 ), plus playerX. For the Y coordinate, it's ( scale * line length ) multiplied by sin( playerAngle + 90 ) plus ( scale * line length ) multiplied by cos( playerAngle + 90 ) plus playerY.

## 14 Experiment with variables

The `update` statement at the very end copies the temporary frame buffer to the screen display... and voila!

There are plenty of variables to experiment with so feel free to change numbers and see what happens. Doing so will provide a great insight into what is going on.

Next month we will add enemies, firing and maybe a few sound effects, too. The Particle Laser is brilliant!

```
# Calculate player position
pX = ( ( radius * cos( pAngle - ( gap / 2 ) ) + centerX ) +
( ( radius * cos( pAngle + ( gap / 2 ) ) + centerX ) ) / 2
pY = ( ( radius * sin( pAngle - ( gap / 2 ) ) + centerY ) +
( ( radius * sin( pAngle + ( gap / 2 ) ) + centerY ) ) / 2
angle = 0

if moveCount > 0 then
    moveCount = moveCount - 1
end
```

```
# move the center of closer objects more
if pX + 2 < gwidth / 2 then // check the players position
    if centerX < ( gwidth / 2 ) + ( gwidth / 20 ) then
        centerX = centerX + 4
        centerY2 = centerY2 + 2
    end
end

if pX - 2 > gwidth / 2 then
    if centerX > ( gwidth / 2 ) - ( gwidth / 20 ) then
        centerX = centerX - 4
        centerY2 = centerY2 - 2
    end
end

if pY + 2 < gheight / 2 then
    if centerY < ( gheight / 2 ) + ( gheight / 20 ) then
        centerY = centerY + 4
        centerY2 = centerY2 + 2
    end
end

if pY - 2 > gheight / 2 then
    if centerY > ( gheight / 2 ) - ( gheight / 20 ) then
        centerY = centerY - 4
        centerY2 = centerY2 - 2
    end
end

colour = yellow
c = cos( pAngle + 90 ) // correct the view angle by 90 degrees
s = sin( pAngle + 90 )
u = gheight / 80 // scale the player ship to the resolution
```

```
# rotate & scale coordinates; draw player ship
polystart
polypot((u*(5 * c) - (u*5 * s) + pX), (u*(5 * s) + (u*(5 * c) + pY))
polypot((u*(5 * c) + pX), (u*(5 * s) + pY))
polypot((0 - (u*2 * s) + pX), (u*(-2 * s) + pY))
polypot((u*(-4 * c) + pX), (u*(-5 * s) + pY))
polypot((u*(-5 * c) - (u*(5 * s) + pX), (u*(-5 * s) + (u*(5 * c) + pY))
polypot((0 - (u*4 * s) + pX), (u*(-4 * s) + pY))
polypot((u*(-7 * c) + pX), (u*(-7 * s) + pY))
polypot((u*(7 * c) + pX), (u*(7 * s) + pY))
polyend
update
repeat
end
```

## WIN! FUZE Special Edition

### Closing date for entries
10 February 2016

With decidedly retro roots, the award-winning FUZE is a programmable computer and electronics workstation. Born out of a passion for programming and love of electronics, the solid aluminium case features an integrated keyboard, a specially designed GPIO header and a breadboard for simple electronics. Housed the Raspberry Pi safely below the keyboard, the FUZE comes complete with FUZE BASIC already installed.

FUZE BASIC is an advanced, modernised version of the BASIC programming language, widely accepted as the easiest beginner language to teach and learn. Featuring a redesigned interface and advanced graphics support, including sprite and image scaling, angle and alpha controls and rotation, FUZE BASIC is fully configured to run with all models of the Raspberry Pi. The whole FUZE system is slick and intuitive, and more than capable of programming web and mobile games.

The FUZE Special Edition pays tribute to home computers of the 1980s like the BBC Micro, and comes complete with a robotic arm kit to integrate with your projects. The FUZE Special Edition also provides you with a projects pack and directs you to plenty of online resources at the FUZE Lair, giving you everything you need to get started. For more information, head over to www.fuze.co.uk.

### Enter the competition

For a chance to win a FUZE T2-SE – a Special Edition with the robotic arm kit – just go to the link below. Answer the simple question provided on that webpage and then add your contact details to enter the competition. The three winners will then be announced in the New Year – good luck!

![](img/0fc17bd4c29dc437e3ac28a53f7559db_77_0.png)

Teaching kids to code

Answer the question on this webpage for a chance to win!

www.linuxuser.co.uk/news/win-a-fuze-se

**TERMS & CONDITIONS**
This competition is open to residents of the United Kingdom and Ireland. Imagine Publishing has the right to substitute the prize for a similar item of equal or higher value. Employees of Imagine Publishing (including freelancers), their relatives or any agents are not eligible to enter. The editor's decision is final and no correspondence will be entered into. Prizes cannot be exchanged for cash. Full terms and conditions are available upon request. By entering the competition you give consent for Imagine Publishing to send you monthly email newsletters and occasional special offers. You can unsubscribe from this at any time by clicking on the unsubscribe link of any email received.

## Internet of Things?

Wireless devices from £9.99 inc VAT

![](img/0fc17bd4c29dc437e3ac28a53f7559db_78_0.png)

wirelessthings.net/lxu-offer
@wirelessthings

## PCI Express LTD

![](img/0fc17bd4c29dc437e3ac28a53f7559db_79_0.png)

TBS is a professional manufacturer of digital TV tuners

Their products include:

- DVB-S/S2 (SD Satellite & HD Satellite)
- DVB-T/T2 (SD Terrestrial & HD Terrestrial)
- DVB-C (SD Cable)
- IPTV Streamer
- USB TV Tuners

With a wide variety of choices:
Single, Dual, Quad Tuner
Common Interface (CI)
And now the all new MINI tuner (7220 below)

All TBS tuners are compatible with Windows 7 Media Center and support Linux with the latest kernel.

## Get the best digital TV tuners for your PC!

![](img/0fc17bd4c29dc437e3ac28a53f7559db_79_1.png)

WORKS ON EUMETSAT

### TBS 6908 Professional HD DVB-S2 Quad Tuner PCIe Card

TBS6908 is a professional level digital satellite TV tuner card with PCI Express interface. It supports not only normal DVB-S2/DVB-S QPSK, BPSK which is supported by normal satellite receivers, but also CCM, ACM, VCM, Multi Input Stream, 16APSK, 32APSK, Generic Stream Mode, which most satellite receiving devices can't support.
With use of dedicated TBS tools, those special streams can be captured. Both Windows BDA driver and Linux driver up to the latest kernel 3.X are ready.
S.R.P £329.95

![](img/0fc17bd4c29dc437e3ac28a53f7559db_79_2.png)

### TBS 6905 HD DVB-S2
Quad Tuner PCIe Card

TBS6905 is a PCI Express interface digital satellite TV tuner card with four tuners for watching and recording FTA (Free To Air) satellite TV on PC. The four tuners allow you to watch TV channels from one transponder or satellite while receiving three other channels from different transponders/satellites at the same time. It’s compatible with Windows 7 Media Center and popular software like MediaPortal, DVBlink, DVBDream, DVBViewer, ProgDVB, SkyNet, T$reader, XBMC and MythTV.
S.R.P £179.95

![](img/0fc17bd4c29dc437e3ac28a53f7559db_79_3.png)

### TBS 6290 DVB-T2/T/C
Dual Tuner Dual CI PCIe Card

TBS6290 is the latest DVB-T2/T PCI Express tuner, it’s equipped with dual tuner and dual CI slots, which allow you to enjoy two live terrestrial TV channels and two different frequencies at the same time, and it supports both reception of FTA (Free to Air) TV channels and encrypted TV channels. TBS6290 can be used as a digital video recorder for recording digital terrestrial TV programs with full HDTV support. With the time-shifting function.
S.R.P £179.95

![](img/0fc17bd4c29dc437e3ac28a53f7559db_79_4.png)

OUR SMALLEST CARD EVER!

### TBS 7220 DVB-T2/T/C mini PCIe Card

TBS 7220 DVB-T2/T/C TV Tuner mini PCIe Card, is a digital terrestrial tuner card with DVB-C function added, which allows you to enjoy Free-to-Air (FTA) digital terrestrial/cable TV and digital stereo radio on PC. TBS 7220 can be used as a digital video recorder for recording digital terrestrial/cable TV programs with full HDTV support. It also enables you to pause a live broadcast & continue from where you left with the time-shifting function. It’s ideal for watching UK Freeview SD and HD. S.R.P £69.95

## CHECK OUT OUR WEBSITE FOR MORE GREAT TBS PRODUCTS
WWW.TBSCARDS.CO.UK

## EXCLUSIVE OFFER

Buy online at www.tbcards.co.uk and receive a 10% discount on any TBS product using code: LINUXUD

Trade Enquiries Welcome
E: mike@pcixex.co.uk

Buy Online:
www.radtv.co.uk
www.valueav.co.uk
www.amazon.co.uk
