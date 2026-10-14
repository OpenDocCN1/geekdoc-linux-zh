
To add the output of our circuit click on New, enter Hwy3 in the Name field, and click on the Output radio-button. Then click on the Advanced button to bring up the Advanced Port Settings window. Click on the Combinatorial radio-button and then the OK button. Now all the inputs and outputs are defined, so click on the Finish button.

At this point, an HDL Editor window will appear (Figure 2.13) with the skeleton of the Trip-Genie logic. You should see the module name and title at the top of the file. These are followed by declarations for the input pins and a single combinational output pin we added previously. Further down in the file is a section intended for logic equations. All we need to do is enter the Boolean equation we derived for the Hwy3 output in the previous chapter. This is typed on line 17 and 18 as follows:

```
Hwy3 = (Hootersville & !Mayberry # (Hootersville & Mayberry) & (SilerCity & !MtPilot);
```

We have used ABEL operators to express the following Boolean operations:

| Boolean Operation | ABEL Operator |
|---|---|
| AND | & |
| OR | # |
| NOT | ! |

Now we have to check to make sure we have not made any simple mistakes. Select the Synthesis → Check Syntax menu item. A small pop-up window will appear informing you that the ABEL code is being examined for errors. Within a few seconds, this window should be replaced by another window stating Check Successful. Click the OK button in this window.

(You are likely to get syntax errors when you first begin to use ABEL for your own designs. Each error will be highlighted in the HDL Editor window and an error message will appear at the bottom of the window. You can get error-free ABEL code examples by selecting the Tools → Language Assistant menu item. A Language Assistant-ABEL window will appear which lists topics on the left-hand side. Click on the + symbols to drill-down to a particular topic. Click on the topic and an ABEL code example for that topic will appear on the right side of the window. You can cut-and-paste the example into your own code and then edit it for your particular design.)

Once we know there are no syntax errors, we can generate a netlist from the ABEL code. The netlist is a distillation of the ABEL code into a set of logic gates and the connections between them. First, click on the Synthesis → Options... menu item. In the ABEL6 window that appears, click on the Chip radio-button and then click OK. This directs the synthesizer to create a netlist

![](img/5124daf79d2807d81e49f49c22f1f8c1_49_0.png)

## Figure 2.13 HDL Editor window with the filled-in Trip-Genie ABEL code skeleton.

for a stand-alone design. (The Macro radio-button is used when the ABEL code describes a logic circuit that is used as part of a larger design.) Then click on the Synthesis → Synthesize menu item to start the compilation process. A small pop-up window will appear informing you that the ABEL code is being synthesized. Within a minute, this window should be replaced by another window stating Synthesis Successful. Click the OK button in this window. The netlist for the Hwy3 output of the Trip-Genie now exists.

Now that the design entry is complete, select File → Save in the HDL Editor window. Then select File → Exit.

Upon returning to the Project Manager window, we must make the TRIP-GENI.ABL file a part of our project. Select the Document → Add... menu item and list items of type ABEL (*.ABL)¹ in the dialog window. Highlight TRIPGENI.ABL and click Open. You should then find TRIPGENI.ABL in the list of files making up the TRIPGENI project (Figure 2.14).

1. You can get all the design examples in this book from the enclosed CD-ROM if you want to avoid reentering them all.

![](img/5124daf79d2807d81e49f49c22f1f8c1_50_0.png)

## Figure 2.14 Project Manager window after the TRIPGENI.ABL file is added to the TRIPG_95 project.

## Entering the Design Using the Schematic Editor

In this section, I will show you how to enter the design for the Hwy3 output of the Trip-Genie using the schematic editor. (You can skip this section if you have already described the design using an ABEL file. I have oriented this schematic-based design toward the XC4000XL FPGA, so you will find it in the TRIPG_40 project.) In the Project Manager window, select Tools → Design Entry → Schematic Editor... (or click on the button in the Flow tab of the Project Manager window) and a schematic editor window will appear. Then name the schematic TRIPGENI.SCH using the File → Save As... menu item.

The first thing we need to do is add the gates for the Hwy3 circuit. Select the Mode → Symbols menu item (or click on the button) and the SC Symbols window will appear with a list of all the types of components we can use. We
