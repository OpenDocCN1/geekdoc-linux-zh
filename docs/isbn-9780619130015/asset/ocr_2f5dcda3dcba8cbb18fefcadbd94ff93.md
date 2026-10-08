+   3 Type cut -d: -f1 programmer | sort | uniq > t2 and press Enter.

+   4 To display the contents of t2, type cat t2 and press Enter.
You see this list of programmer numbers:

101  
102  
103  
104  
105  
106  
107  
108  
109  
110  
111  
112  
113  
114

Now that t1 and t2 are sorted in the same order, you can match them. Use the comm command to select the lines from t1 that do not match lines in t2, and redirect the output to another file, t3, which lists programmer numbers of all programmers who are not assigned to projects.

+   5 Type comm -13 t1 t2 > t3 and press Enter.

+   6 To display the programmer numbers for programmers who are not working on projects, type cat t3 and press Enter.
You see this list of programmer numbers:

108  
111  
113  
114

To display the names of unassigned programmers, you can now sort the programmer file in programmer_number order and write the output to t4.

+   7 Type sort -t: -o:1 -o t4 programmer and press Enter.
Now use the join command to match programmer_numbers in t4 and t3, and redirect the output to t5, which contains the names of all programmers who are not assigned to a project.

+   8 Type join -t: -j11 -j2 1 -o 1.2 -o 1.3 -o 1.4 t4 t3 > t5 and press Enter.