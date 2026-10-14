# Modular Designs and Hierarchy

# Objectives

+   - Describe the advantages of logic encapsulation and hierarchical design.
+   - Show how to describe logic modules and interconnect them in a hierarchical fashion using a HDL.
+   - Show how to describe logic modules and interconnect them in a hierarchical fashion using a schematic editor.

# Discussion

By now, you have built combinatorial logic circuits and tested them by using the simulator and by downloading them into the XS40 or XS95 Board. It has all been so simple! So simple, in fact, that you might be asking the question, "Since the computer can figure out the logic design from just the truth table, what do you need me for?" Well, maybe we don't! On the other hand, we have calculators but we still have accountants. The important fact is that the tedious calculations have been automated, leaving us with the more challenging tasks to perform that computers do not yet do so well. For example, accountants now spend less time adding numbers and more time figuring out neat ways to evade the tax regulations. Likewise, you can spend more time thinking up neat circuits and less time mechanically grinding out the details.

However, the computer-aided design programs will always have limitations, so you cannot completely ignore the details of how the gates are connected to build a design. Having knowledge of how logic is transformed and minimized allows you to check the output from the programs and determine if some terrible mistake is being made. At other times, the CAD programs will fail to find a solution even though you know one exists. In these cases, you will have to go in by hand and give a more detailed specification to help the CAD program figure it all out.

More detailed specifications are also needed if you are pushing the limits of your devices. For example, you may be trying to build a circuit that performs