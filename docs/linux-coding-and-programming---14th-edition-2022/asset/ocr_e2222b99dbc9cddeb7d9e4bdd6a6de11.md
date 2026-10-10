# # C++ Maths

Programming is mathematical in nature and as you might expect, there’s plenty of built-in scope for some quite intense maths. C++ has a lot to offer someone who’s implementing mathematical models into their code. It can be extremely complex or relatively simple.

# ## C++ = MC2

The basic mathematical symbols apply in C++ as they do in most other programming languages. However, by using the C++ Math Library, you can also calculate square roots, powers, trig and more.

+   **STEP 1** C++’s mathematical operations follow the same patterns as those taught in school, in that multiplication and division take precedence over addition and subtraction. You can alter that though. For now, create a new file and enter:
+   ```c
+   #include <iostream>
+   using namespace std;
+   
+   int main ()
+   {
+       float numbers = 100;
+   
+       numbers = numbers + 10; // This adds 10 to the initial 100
+       cout << numbers << "\n";
+   
+       numbers = numbers - 10; // This subtracts 10 from the new 110
+       cout << numbers << "\n";
+   }
+   ```
+   **STEP 3** Multiplication and division can be applied as such:
+   ```c
+   #include <iostream>
+   using namespace std;
+   
+   int main ()
+   {
+       float numbers = 100;
+   
+       numbers = numbers * 10; // This multiplies 100 by 10
+       cout << numbers << "\n";
+   
+       numbers = numbers / 10; // And this divides 1000 by 10
+       cout << numbers << "\n";
+   }
+   ```

![](bbox=[0.06, 0.61, 0.93, 0.75])

+   **STEP 2** While simple, it does get the old maths muscle warmed up. Note that we used a float for the numbers variable. While you can happily use an integer, if you suddenly started to use decimals, you would need to change to a float or a double, depending on the accuracy needed. Run the code and see the results.
+   **STEP 4** Again, execute the simple code and see the results. While not particularly interesting, it’s an introduction to C++ maths. We used a float here, so you can play around with the code and multiply by decimal places, as well as divide, add and subtract.

![](bbox=[0.06, 0.85, 0.93, 0.94])

138 www.bdnpublications.com