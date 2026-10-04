An arithmetic comparison{$a < 2}

A string comparison {$string != "OK"}

The results of a command [eof $inputFile]

A variable with a numeric {$AnalysisResult} value. Zero (0) is considered false, and nonzero values are true.

body1 The body of code to evaluate if the first test evaluates as true.

elseif If testExpression1 is false, evaluate testExpression2.

testExpression2 A second test to evaluate if the first test evaluates to false.

body2 The body of code to evaluate if the second test evaluates as true.

?else bodyN If all evaluate false, this body of code will be evaluated.

In the following example, the placement of the curly braces ({}).
The Tcl Style Guide describes the preferred format for if, for, proc, and commands. It recommends that you place the left curly brace of the command and place the body on the next lines, indented four spaces. The final, right curly brace should go on a line by itself, indented even with the opening command. This makes the code less dense (and more easily read).

Putting the test and action on a single line is syntactically correct Tcl code but can cause maintenance problems. You will need to make some multiline code statements, mixing multiple and single-line commands can make the action statements hard to find. Also, what looks simple when you start writing some code may need to be expanded as you discover more about the problem you are solving. You may as well start with the code laid out to support new lines of code.

Because of the way a Tcl command is evaluated, a left curly brace must be at the end of a line of code, not on a line by itself. The reasons for this are discussed in Chapter 4.