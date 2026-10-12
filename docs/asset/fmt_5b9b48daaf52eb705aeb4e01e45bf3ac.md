
#### op_to_source

```
i:
/*
 * IBM Performance Inspector
 * Copyright (c) International Business Machines Corp., 2003
 *
 * This library is free software; you can redistribute it and/or modify
 * it under the terms of the GNU General Public License as published
 * by the Free Software Foundation; either version 2.1 of the License, or
 * (at your option) any later version.
 *
 * This library is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See
 * the GNU General Public License for more details.
 *
 * You should have received a copy of the GNU General Public License
 * along with this library; if not, write to the Free Software
 * Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA 02111-1307 USA
*/
              :
      #include <stdio.h>
      #include <stdlib.h>
      #include <unistd.h>
      int One(unsigned long long cps);
      int Two(unsigned long long cps);
      int Four(unsigned long long cps);
      int Eight(unsigned long long cps);
      int Sixteen(unsigned long long cps);
      int ThirtyTwo(unsigned long long cps);
      int SixtyFour(unsigned long long cps);



int val = 0;
     /********************************************************/
        10 0.003%    580 0.000% : void pc50() { /* pc50 total:  153902 52.31% 40667094 52.46% */
              :         int i;
   119226 40.52% 29583773 38.16% :         for(i = 0; i < 5000; i++) {
    34613 11.76% 11071427 14.28% :                val = val + i;
              :         }
          53 0.018%  11314 0.014% :         int i;
              :                /***************************************************/
          8 0.002%    290 0.000% : void pc25() { /* pc25 total:    70463 23.95% 18765427 24.20% */
              :         int i;
    60711 20.63% 16897936 21.79% :         for(i = 0; i < 2500; i++) {
     9693 3.295% 1851007 2.387% :                val = val + i;
              :         }
          51 0.017%  16194 0.020% :         int i;
              :                /***************************************************/
         13 0.004%   5455 0.007% : void pc15() { /* pc15 total:    43572 14.81% 11245713 14.50% */
              :         int i;
    39415 13.39% 11069245 14.27% :         for(i = 0; i < 1500; i++) {
      4046 1.375%  136253 0.175% :                val = val + i;
:}

98 0.033% 34760 0.044% :}
*:**** ** ** ** *** ** *** ** ** *** ** ** */
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

#### op_merge
