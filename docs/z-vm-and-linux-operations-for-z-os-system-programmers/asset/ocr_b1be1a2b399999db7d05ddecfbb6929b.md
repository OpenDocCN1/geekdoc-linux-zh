in batch mode. The system operator generates the batch machine by either of the following methods:

+   Entering the BATCH parameter in the PARM field of the IPL command
+   Specifying the NOSPROF parameter of the IPL command and entering the CMSBATCH command when the VM READ status appears.

After each job is executed, the batch facility IPLs itself, thereby providing a continuously processing batch machine. The batch processor IPLs itself by using the PARM option of the CP IPL command followed by a character string that CMS recognizes as peculiar to a batch virtual machine performing its IPL. Jobs are sent to the batch machine's virtual card reader from user terminals and executed sequentially. When no jobs are waiting for execution, the CMS batch facility remains in a wait-state, ready to execute a user job. The CMS batch facility is particularly useful for compute-bound jobs such as assemblies and compilations and for execution of large user programs, because interactive users can continue working at their terminals while their time-consuming jobs are run in another virtual machine. The system programmer controls the batch facility virtual machine environment by resetting the CMS batch facility machine's system limits, by writing routines that handle special installation input to the batch facility, and by writing exec procedures that make the CMS batch facility easier to use.

> Note: For in-depth information about how to use the CMS Batch Facility, refer to the CMS Planning and Administration, SC24-6078 at:
> http://publibz.boulder.ibm.com/epubs/pdf/hcsq2b10.pdf

# Simulating batch jobs in Linux

This section gives you a very simple overview of how to use scripts to simulate batch-like processing. You can also schedule cron to run the scripts during the night, for example, to run daily sales reports.

The scenario in this section makes use of shell scripting, a language interpreted by many Linux shells⁷, to control the batch behavior of the processes. This controlling script runs one program at a time. We wrote two simple programs to sort the words of text files: one in natural order and the other in reverse order.

The script is shown in Example 5-52 on page 278. It calls all programs found in the ./batch folder, our sorting programs. Each of the programs has its corresponding input file in our the ./input folder (where we placed the files for sorting) and each output is sent to our ./output folder. The only constraint to

⁷ A shell is a program that interprets user inputs, calls the corresponding system's commands, and displays the output of that command. It is the user interface shown in Linux consoles after you log in.