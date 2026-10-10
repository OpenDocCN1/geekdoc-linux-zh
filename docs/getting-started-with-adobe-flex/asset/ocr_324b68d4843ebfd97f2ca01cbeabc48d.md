| DataType | Description | Default Value | Example |
| :--- | :--- | :--- | :--- |
| String | Used for text. Can have one or more characters enclosed in single quote or double quote | null | var mystir:String="hello"; |
| Number | A numeric value that can be a fraction | NaN (Not a Number) | var mynum:Number=3.25; |
| Uint | Unsigned integer. It can range from 0 to 4,294,967,295 | 0 | var myuint:uint=35; |
| Int | Any integer. It can range from -2,147,483,648 to +2,147,483,647 | 0 | var myint:int=-2.5; |
| Boolean | A true or false value. Possible values include true and false. | false | var isCircle:Boolean= true; |
| Void | A special value used with functions to denote that the function returns nothing. It has the value undefined. | undefined | function doNothing():void{
} |

Table 3.1 - ActionScripts data types

# 3.3.4 ActionScript Classes and Objects

In order to create a class in Flex, you create a new ActionScript class that has a .as extension. Using Flex Builder, choose File -> New -> ActionScript Class as shown in Figure 3.3.