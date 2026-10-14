# Programmable Logic
Design Techniques

# Objectives

+   - Discuss the advantages of designing with programmable logic.
+   - Discuss the evolution of programmable logic.
+   - Introduce the use of the XILINX Foundation Series 1.5 Software tools for programmable logic design.

# Discussion

# The Advantages of Computer-aided Design and
Programmable Logic

You can build digital circuits of up to several hundred gates using SSI and medium-scale integration (MSI) ICs. As you saw in the last chapter, these ICs are typically plugged into a breadboard and connections are made between them using 22- or 24-gauge hookup wire. Then switches and LEDs are connected to the inputs and outputs, respectively, and the circuit is exercised to see if it operates correctly. As you have probably already realized, there are a lot of things wrong with this method of building circuits:

+   - Cutting and stripping wires to make connections between ICs is time consuming.
+   - Wires are often plugged into the wrong place, so a lengthy check must be made to find the error in order to make the circuit work.
+   - With a limited budget, you may not have every type of TTL IC immediately available to you.
+   - Once your circuit works, you have to tear it apart to make room for the next design. Using a previously built circuit as a part of your current design is difficult to do.

In addition to the problems involved in physically building the circuit, you are also forced to use primitive tools when designing the circuit. For combinatorial circuits, you begin with a truth table and derive an efficient logic circuit from