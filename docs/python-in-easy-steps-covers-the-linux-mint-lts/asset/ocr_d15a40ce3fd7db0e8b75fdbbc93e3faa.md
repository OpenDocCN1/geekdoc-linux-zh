# Adding runtime functionality

Having created code to initialize dynamic properties here, you can now add runtime functionality to respond to clicks on the Button widgets during execution of the program.

+   1. Modify the program here by inserting one more new section just before the final loop statement, which begins by making the sample() function available from the “random” module
+      
+      # Dynamic Properties:
+      from random import sample

![](bbox=[0.12, 0.4, 0.17, 0.46])

lotto.py

+   2. Next, define a function that generates and assigns six unique random numbers to the small Labels and reverses the state of both Buttons
+      
+      def pick():
+          nums = sample( range( 1, 59 ), 6 )
+          label1.configure( text = nums[0] )
+          label2.configure( text = nums[1] )
+          label3.configure( text = nums[2] )
+          label4.configure( text = nums[3] )
+          label5.configure( text = nums[4] )
+          label6.configure( text = nums[5] )
+          getBtn.configure( state = DISABLED )
+          resBtn.configure( state = NORMAL )

+   3. Now, define a function to display an ellipsis on each small Label and revert both Buttons to their initial states
+      
+      def reset():
+          label1.configure( text = '...' )
+          label2.configure( text = '...' )
+          label3.configure( text = '...' )
+          label4.configure( text = '...' )
+          label5.configure( text = '...' )
+          label6.configure( text = '...' )
+          getBtn.configure( state = NORMAL )