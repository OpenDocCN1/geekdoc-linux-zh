Testing should be automated as much as possible. This is particularly easy to do for non-GUI programs written in the style of the `Linux/Unix` tools: programs that read standard input or named files, and write to standard output and standard error. At the very least, testing can be done with simple shell scripts. More involved testing is usually done with a separate `test` subdirectory and the `make` program.

Software testing is a whole subfield in itself, and we don't expect to do it justice here; rather our point is to make you aware that testing is an integral part of development and often the motivating factor for using your debugging skills! Here is a **very** brief summary list:

+   * Design the test along with the feature.
+   * Test boundary conditions: Make sure the feature works both inside and at valid boundaries and that it fails correctly outside them. (For example, the `sqrt()` function has to fail when given a negative argument.)
+   * Use assertions in your code (see Section 12.1, "Assertion Statements: `assert()`", page 428), and run your tests with the assertions enabled.
+   * Create and reuse test scaffolding.
+   * Save failure cases for regression testing.
+   * Automate testing as much as possible.
+   * Print a count of failed tests so that success or failure, and the degree of failure, can be determined easily.
+   * Use code coverage tools such as `gcov` to verify that your test suite exercises all of your code.
+   * Test early and test often.
+   * Study software-testing literature to improve your ability to develop and test software.

# ## 15.7 Debugging Rules

Debugging isn't a "black art." Its principles and techniques can be learned, and consistently applied, by anyone. To this end, we highly recommend the book *Debugging*