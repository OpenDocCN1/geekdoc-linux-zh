```
:}

98 0.033% 34760 0.044% :}
*:**** ** ** ** ** *** ** *** ** ** *** ** ** */
9 0.003% 116 0.000% :void pc10() { /* pc10 total: 26148 8.888% 6818423 8.795% */
: int i;
: }
20936 7.116% 5432322 7.008% : for (i = 0; i < 1000; i++) {
5154 1.752% 1365913 1.762% : val = val + i;
:}
49 0.016% 19132 0.024% :}
*:**** ** ** ** *** ** *** ** *** ** *** ** *** ** *** ** */

0.028% 22107 0.028% :*/int main(int argc, char *argv[]) { /* main total: 84
: int i;
: int iter;
:
: if (argc == 2) {
: iter = atoi(argv[1]);
: }
: else {
: fprintf (stderr, " Usage: watch iter\n");
: fflush (stderr);
: exit(0);
: }
:
: val = 0;
47 0.015% 10143 0.013% : for (i = 0; i < iter; i++) {
5 0.001% 1011 0.001% : pc50();
11 0.003% 6072 0.007% : pc25();
9 0.003% 1313 0.001% : pc15();
12 0.004% 3568 0.004% : pc10();
:}
:
: fprintf (stderr, " val = %d\n", val);
: return(0);
:}
:
/* * Total samples for file : "/piperf/src/pi_watch.c"
* 294169 100.0% 77518764 100.0%*/

/*
* Command line: cp_to_source --source-dir=/piperf/src --output-dir=/temp /piperf/bin/pi_watch
*
* Interpretation of command line:
* Output annotated source file with samples
* Output all files
*
* Cpu type: PIII
* Cpu speed (MHz estimation) : 662.229
*
Counter 0 counted CPU_CLK_UNHALTED events (clock's processor is not halted) with a unit mask of 0x00 (No unit mask) count 400000
* Total samples : 294169

Counter 1 counted DATA_MEM_REFS events (all memory references, cacheable and non) with a unit mask of 0x00 (No unit mask) count 1000
* Total samples : 77518764
*/
```