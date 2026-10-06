# # Branching
# 13

+   CHAPTER CONTENTS
13.1 Avoiding Branches ................................................ 242
    13.1.1 Extra Work and Masking ................................................. 243
    13.1.2 Combining and Rearranging Branches ................................ 245
13.2 Improving Prediction ................................................................... 247
    13.2.1 Profile Guided Optimization ............................................ 248
References ....................................................................................... 249

As discussed in Chapter 1, the instruction pointer contains the address of the next instruction to be executed. After the current instruction is executed, the instruction pointer increments to the next instruction, and so on. A branch introduces a deviation from this incremental behavior. Instead of incrementing to the next instruction, the branching instruction loads the instruction pointer to the address of an instruction at a different code.

Every branch can be classified as either conditional or unconditional. As the names imply, a conditional branch may or not change the instruction flow, while an unconditional branch will always change the flow. Most tend to associate the concept of branching with the first category, conditional branches, since these are the most visible forms. This kind of branch corresponds to the conditional and looping constructs exposed by programming languages, such as if or for statements. The other kind of branch, an unconditional branch, corresponds to control flows, such as calling or returning from a function.

Due to the superscalar nature of the execution pipeline in Intel® processors, comprised of many parallel execution units, it is more efficient to keep the pipeline full, executing multiple instructions simultaneously, than to let instructions trickle in. In an attempt to keep the execution pipeline fully, the processor, in hardware, performs an optimization referred to as speculative execution. With speculative execution, upon approaching a branch, the processor predicts which branch will be taken. It will then use this guess to begin, possibly prematurely, executing the instructions from the predicted branch path. In the case of a correct guess, referred to as a branch hit, the instructions from both