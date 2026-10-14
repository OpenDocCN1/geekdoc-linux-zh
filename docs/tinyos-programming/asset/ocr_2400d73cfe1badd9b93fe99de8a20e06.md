+   3.28 The Receive interface 39
+   3.29 The signature of PoolC 41
+   3.30 CC2420 packet header 42
+   3.31 The dreaded "packed" attribute in the 1.x MintRoute library 43
+   3.32 The CC2420 header 44
+   3.33 TinyError.h, a typical nesC header file 45
+   3.34 Including a header file in a component 45
+   3.35 Indirectly including a header file 46
+   3.36 Fancy.nc: C preprocessor example 46
+   3.37 FancyModule.nc: C preprocessor pitfalls 47
+   3.38 Fancy.h: the reliable way to use C preprocessor symbols 47
+   3.39 Using a C library function 47
+   4.1 Signature of part of the CC1000 radio stack 49
+   4.2 The PowerupToggleAppC configuration revisited 51
+   4.3 C code generated from the PowerupToggleAppC configuration 51
+   4.4 The LedsC configuration 52
+   4.5 CC2420ReceiveC's use of the as keyword 53
+   4.6 Naming generic component instances 54
+   4.7 MainC and LedsP 55
+   4.8 Valid alternate of PowerupToggleAppC 55
+   4.9 Invalid alternate of PowerupToggleAppC 55
+   4.10 LedsC revisited 56
+   4.11 BlinkC signature 56
+   4.12 The RandomC configuration 57
+   4.13 The RandomMlcgC signature 58
+   4.14 Seed initialization in RandomMlcgP 59
+   4.15 ActiveMessageC for the CC2420 61
+   4.16 The signature of CC2420ActiveMessageC 62
+   4.17 Fan-out on CC2420TransmitC's Init 63
+   4.18 StdControl and SplitControl initialization interfaces 64
+   4.19 Why the metaphor of "wires" is only a metaphor 65
+   4.20 The combine function for error_t 66
+   4.21 Fan-out on SoftwareInit 67
+   4.22 Resulting code from fan-out on SoftwareInit 67
+   4.23 AMSenderC signature 68
+   4.24 RadioCountToLedsAppC 68
+   4.25 PoolC 69
+   4.26 Exposing a generic component instance as a singleton 70
+   5.1 The main TinyOS scheduling loop from SchedulerBasicPnc 72
+   5.2 A troublesome implementation of a magnetometer sensor 76
+   5.3 Signal handler that can lead to an infinite loop 77
+   5.4 An improved implementation of FilterMagC 77
+   6.1 Anti-theft: simple flashing LED 80
+   6.2 The Leds interface 80