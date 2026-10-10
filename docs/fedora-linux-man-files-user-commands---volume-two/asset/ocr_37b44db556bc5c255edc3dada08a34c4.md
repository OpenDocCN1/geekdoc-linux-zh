The input/output statements are as follows:

+   **close(*file* [, *how*])**
+   Close *file*, pipe or co-process. The optional *how* should only be used when closing one end of a two-way pipe to a co-process. It must be a string value, either **to** or **from**.

+   **getline**
+   Set **$0** from next input record; set **NF, NR, FNR, RT**.

+   **getline <** *file*
+   Set **$0** from next record of *file*; set **NF, RT**.

+   **getline** *var*
+   Set *var* from next input record; set **NR, FNR, RT**.

+   **getline** *var* **<** *file*
+   Set *var* from next record of *file*, **RT**.

+   *command* **| getline** [*var*]
+   Run *command* piping the output either into **$0** or *var*, as above, and **RT**.

+   *command* **& getline** [*var*]
+   Run *command* as a co-process piping the output either into **$0** or *var*, as above, and **RT**. Co-processes are a *gawk* extension. (*command* can also be a socket. See the subsection **Special File Names**, below.)

+   **next**
+   Stop processing the current input record. The next input record is read and processing starts over with the first pattern in the *AWK* program. Upon reaching the end of the input data, *gawk* executes any **END** rule(s).

+   **nextfile**
+   Stop processing the current input file. The next input record read comes from the next input file. **FILENAME** and **ARGIND** are updated, **FNR** is reset to *1*, and processing starts over with the first pattern in the *AWK* program. Upon reaching the end of the input data, *gawk* executes any **END** rule(s).

+   **print**
+   Print the current record. The output record is terminated with the value of **ORS**.

+   **print** *expr*-list
+   Print expressions. Each expression is separated by the value of **OFS**. The output record is terminated with the value of **ORS**.

+   **print** *expr*-list **>** *file*
+   Print expressions on *file*. Each expression is separated by the value of **OFS**. The output record is terminated with the value of **ORS**.

+   **printf** *fmt*, *expr*-list
+   Format and print. See **The printf Statement**, below.

+   **printf** *fmt*, *expr*-list **>** *file*
+   Format and print on *file*.

+   **system**(*cmd*-line)
+   Execute the command *cmd-line*, and return the exit status. (This may not be available on non-POSIX systems.)