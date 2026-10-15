# WORK WITH ARRAYS

Visual Basic .NET contains a number of functions for manipulating arrays. You can use these functions to sort the array, remove items, and determine the size of the array.

The LBound and UBound functions provide the index of the lower- and upper-most position of the array. Pass the array as the only parameter to either of these functions to return an integer specifying the bound. You use LBound for compatibility with Visual Basic 6 and earlier versions, but an array in VB .NET always begins with index 0, LBound always returns 0. UBound returns the last index of the array. For example, if you make the array declaration Dim myArray(5) As Integer, UBound(myArray) returns 5. You can use this in methods where you have a parameter in an array, but you do not know its size. For example, For x = 0 To UBound(myArray) loops through any array with the name myArray.

The Array object exposes a Sort method. Pass an array to Sort for a standard alphanumeric sort, for example, Array.Sort(myArray). The method sorts the items in the array and saves them back into the same array. The Sort method only supports one-dimensional arrays.

The Array object also exposes a BinarySearch method. BinarySearch locates an individual item in the array. Pass the array and the key to find to locate as the two arguments to the method. For example, Array.BinarySearch(myArray, "John"). You must ensure that the key value you pass to the method is the same type as the objects in the array, meaning if you define the array as an array of Date variables, you must pass a Date variable as the key value. The method returns an integer that specifies the index of the item. A value of less than zero means the item does not exist in the array.

# WORK WITH ARRAYS

![](bbox=[0.05, 0.49, 0.42, 0.82])

![](bbox=[0.52, 0.49, 0.92, 0.82])

+   SET UP THE ARRAY
+   1 Create a new project or open an existing one.
+   2 Create or open the method where the loop needs to execute.
+   3 Declare and fill the array with values.
+   Note: See the section "Create an Array" for information on how to create an array.

+   SORT THE ARRAY VALUES
+   4 Type Array.Sort(myArray), replacing myArray with the name of your array.
+   5 Type the code to work with or display the results.
+   The example above uses a For loop to display all of the values.