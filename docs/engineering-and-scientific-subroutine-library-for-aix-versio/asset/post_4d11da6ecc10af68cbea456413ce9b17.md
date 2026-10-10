
## Concerns about Lengths of Transforms

The length of the transform you can use in your program depends on the limits of the addressability of your processor.

## Determining an Acceptable Length of a Transform

To determine acceptable lengths of the transforms in the Fourier transform subroutines, you have several choices. First, you can use the formula or table of values in “Acceptable Lengths for the Transforms” to choose a value. Second, ESSL’s input-argument error recovery provides a means of determining an acceptable length of the transform. It uses the optionally-recoverable error 2030. For details, see “Providing a Correct Transform Length to ESSL” on page 38.

## Acceptable Lengths for the Transforms

Use the following formula to determine acceptable transform lengths:

$$n = (2^h) (3^i) (5^j) (7^k) (11^m) \quad \text{for} \quad n \leq 37748736$$

where:
- $h = 1, 2, ..., 25$
- $i = 0, 1, 2$
- $j, k, m = 0, 1$

Figure 13 on page 744 lists all the acceptable values for transform lengths in the Fourier transform subroutines.

| 2 | 4 | 6 | 8 | 10 | 12 | 14 | 16 | 18 |
|---|---|---|---|----|----|----|----|----|
| 20 | 22 | 24 | 28 | 30 | 32 | 36 | 40 | 42 |
| 44 | 48 | 56 | 60 | 64 | 66 | 70 | 72 | 80 |
| 84 | 88 | 90 | 96 | 110 | 112 | 120 | 126 | 128 |
| 132 | 140 | 144 | 154 | 160 | 168 | 176 | 180 | 192 |
| 198 | 210 | 220 | 224 | 240 | 252 | 256 | 264 | 280 |
| 268 | 308 | 320 | 330 | 336 | 352 | 360 | 384 | 396 |
| 420 | 440 | 448 | 462 | 480 | 504 | 512 | 528 | 560 |
| 576 | 616 | 630 | 640 | 660 | 672 | 704 | 720 | 768 |
| 770 | 792 | 840 | 880 | 896 | 924 | 960 | 990 | 1008 |
| 1024 | 1056 | 1120 | 1152 | 1232 | 1260 | 1280 | 1320 | 1344 |
| 1386 | 1408 | 1440 | 1536 | 1540 | 1584 | 1680 | 1760 | 1792 |
| 1848 | 1920 | 1980 | 2016 | 2048 | 2112 | 2240 | 2304 | 2310 |
| 2464 | 2520 | 2560 | 2640 | 2688 | 2772 | 2816 | 2880 | 3072 |
| 3080 | 3168 | 3264 | 3360 | 3520 | 3584 | 3696 | 3840 | 4032 |
| 4096 | 4224 | 4480 | 4608 | 4620 | 4928 | 5040 | 5120 | 5280 |
| 5376 | 5544 | 5632 | 5760 | 6144 | 6160 | 6336 | 6720 | 6930 |
| 7040 | 7168 | 7392 | 7680 | 7920 | 8064 | 8192 | 8448 | 8960 |
| 9216 | 9240 | 9856 | 10080 | 10240 | 10560 | 10752 | 11088 | 11264 |
| 11520 | 12288 | 12320 | 12672 | 13440 | 13860 | 14080 | 14336 | 14784 |
| 15360 | 15840 | 16128 | 16384 | 16896 | 17920 | 18432 | 18480 | 19712 |
| 20160 | 20480 | 21120 | 21504 | 22176 | 22528 | 23040 | 24576 | 24640 |
| 25344 | 26880 | 27720 | 28160 | 28672 | 29568 | 30720 | 31680 | 32256 |
| 32768 | 33792 | 35840 | 36864 | 36960 | 39424 | 40320 | 40960 | 42240 |
| 43008 | 44352 | 45056 | 46080 | 49152 | 49280 | 50688 | 53760 | 55440 |
| 56320 | 57344 | 59136 | 61440 | 63360 | 64512 | 65536 | 6784 | 71680 |
| 73728 | 73920 | 78848 | 80640 | 81920 | 84480 | 86016 | 88704 | 90112 |
| 92160 | 98304 | 98560 | 101376 | 107520 | 110880 | 112640 | 114688 | 118272 |
| 122880 | 126720 | 129024 | 131072 | 135168 | 143360 | 147456 | 147840 | 157696 |
| 161280 | 163840 | 168960 | 172032 | 177408 | 180224 | 184320 | 196608 | 197120 |
| 202752 | 215040 | 221760 | 225280 | 229376 | 236544 | 245760 | 253440 | 258048 |
| 262144 | 270336 | 286720 | 294912 | 295680 | 315392 | 322560 | 327680 | 337920 |
| 344064 | 354816 | 360448 | 368640 | 393216 | 394240 | 405504 | 430080 | 443520 |
| 450560 | 458752 | 473088 | 491520 | 506880 | 516996 | 524288 | 540672 | 573440 |
| 589924 | 591360 | 630784 | 645120 | 655360 | 675840 | 688128 | 709632 | 720896 |
| 737280 | 78432 | 788480 | 811008 | 860160 | 887040 | 901120 | 917504 | 946176 |
| 983040 | 1013760 | 1032192 | 1048576 | 1081344 | 1146880 | 1179648 | 1182720 | 1261568 |
| 1290240 | 1310720 | 1351680 | 1376256 | 1419264 | 1441792 | 1474560 | 1572864 | 157660 |
| 1622016 | 1720320 | 1774080 | 1802240 | 1835008 | 1892352 | 1966080 | 2027520 | 2064384 |
| 2097152 | 2162688 | 2293760 | 2359296 | 2365440 | 2523136 | 2580480 | 2621440 | 2703360 |
| 2752512 | 2835828 | 2883584 | 2949120 | 3145728 | 3153920 | 3244032 | 3440640 | 3548760 |
| 3604480 | 3670016 | 3784704 | 3932160 | 4055040 | 412868 | 4159304 | 4325376 | 4587520 |
| 4718592 | 4730880 | 504572 | 516208 | 5242880 | 5406720 | 5505808 | 5677056 | 5767168 |
| 5899240 | 6291456 | 6307840 | 6480064 | 6881280 | 7096320 | 7208960 | 7340032 | 7569408 |
| 7843200 | 8110080 | 8257536 | 8388608 | 8650752 | 9175040 | 9437184 | 9461760 | 10092544 |
| 10321920 | 10485760 | 10813440 | 11010048 | 11354112 | 11534336 | 11796480 | 12582912 | 12615680 |
| 12976128 | 13762560 | 14192640 | 14417920 | 14680064 | 15138816 | 15728640 | 16220160 | 16515072 |
| 16777216 | 17301504 | 18350080 | 18874368 | 18923520 | 20185088 | 20643840 | 20971520 | 21626880 |
| 22020096 | 22788224 | 2366872 | 23592960 | 25165824 | 25231360 | 25942256 | 25752120 | 28385280 |
| 28835840 | 29360128 | 30277360 | 31457280 | 32440320 | 33030144 | 33554432 | 34603008 | 36700160 |

Figure 13. Table of Acceptable Lengths for the Transforms

## Understanding Auxiliary Working Storage Requirements

Auxiliary working storage is required by the Fourier transform subroutines and by the SCONF, SCORF, and SACORF subroutines. This storage is provided through the calling sequence arguments `aux`, `aux1`, and `aux2`. The sizes of these storage areas are specified by the calling sequence arguments `naux`, `naux1`, and `naux2`, respectively.

- **AUX1:** The $aux1$ array is used for storing tables and other parameters when you call a Fourier transform, convolution, or correlation subroutine for initialization with $init = 1$. The initialized $aux1$ array is then used on succeeding calls with $init = 0$, when the computation is actually done. You should not use this array between the initialization and the computation.
- **AUX and AUX2:** The $aux$ and $aux2$ arrays are used for temporary storage during the running of the subroutine and are available for use by your program between calls to the subroutine.
- **AUX3:** The $aux3$ argument is provided for migration purposes only and is ignored.

### Initializing Auxiliary Working Storage

In many of those subroutines requiring $aux1$ auxiliary working storage, two invocations of the subroutines are necessary. The first invocation initializes the working storage in $aux1$ for the subroutine, and the second performs the computations. (For an explanation of auxiliary working storage, see Understanding Auxiliary Working Storage later.) As a result, the working storage in $aux1$ should not be used by the calling program between the two calls to the subroutine. However, it can be reused after intervening calls to the subroutine with different arguments.

If you plan to repeat a computation many times using the same set of arguments, you only need to do one initialization of the $aux1$ array; that is, the initialized $aux1$ array can be saved and reused as many times as needed for the computation.

If you plan to perform different computations, with different sets of arguments (except for input argument $x$), you need to do an initialization for each different computation; that is, you initialize the various $aux1$ arrays for use with the different computations, saving and reusing them until they are not needed any more.

### Determining the Amount of Auxiliary Working Storage That You Need

To determine the size of auxiliary storage, you have several choices. First, you can use the formulas provided in each subroutine description. Second, ESSL's input-argument error recovery provides a means of determining the minimum size you need for auxiliary storage. It uses the optionally-recoverable error 2015. For details, see "Using Auxiliary Storage in ESSL" on page 32. Third, you can have ESSL dynamically allocate $aux$ and $aux2$. For details, see "Dynamic Allocation of Auxiliary Storage" on page 33.

### Performance and Accuracy Considerations

The following sections explain the performance and accuracy considerations for the Fourier transforms, convolution, and correlation subroutines. For further details about performance and accuracy, see Chapter 2, "Planning Your Program," on page 25.
