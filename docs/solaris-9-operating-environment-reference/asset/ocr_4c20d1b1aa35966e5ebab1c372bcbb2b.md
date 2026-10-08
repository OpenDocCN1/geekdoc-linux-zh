# 42

AMT Test Program -- 32 bit application
======================

Test 1- stack Side Boundary Test
TEST PASSED

Test 2- Data Side Boundary Test.
PASS: Successful read/write in data area.
TEST 2 PASSED

Test 3- Text Area Not Writeable
Verify that a write to the text space does not cause a write to the executable file from which it came, or to another process which shares that text.
PASS: Caught the segmentation fault, meaning we can't write to area.
TEST 3 PASSED

Test 4- Memory Not Shared After Write
Verify that anonymous memory initially shared by two processes (e.g. after a fork) is not shared after either process writes to it.
TEST 4 PASSED

Test 5- Memory Allocation Is Not Shared
Verify that newly allocated memory in one of two processes created by forking does not result in newly allocated memory in the other.
Parent address of hole before child change: 00024818
Child end of hole before change: 00024818
Child end of hole after change: 00026818
Parent address of hole after child change: 00024818
PASS: Hole is same size in parent.
TEST 5 PASSED

TESTS SUCCEEDED
mopoke$

# Exit Status

+   - 0 All tests passed.
- >0 Count of the number of tests that failed.
- <0 Incorrect command-line argument.