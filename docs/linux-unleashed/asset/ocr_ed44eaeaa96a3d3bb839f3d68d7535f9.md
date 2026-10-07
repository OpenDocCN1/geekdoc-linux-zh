However, displayed formulas are denoted using two consecutive $ symbols, as in

The equation $$2+3=x$$ must evaluate to $$x=5$$. which produces the following:

The equation

2+3=x

must evaluate to

x=5.

Table 19.1 shows some of the math symbols that TeX can generate, their associated com-mands, and their meaning.

**TABLE 19.1. SOME OF THE MATH SYMBOLS THAT TeX CAN GENERATE.**

| Symbol | TeX Command | Meaning |
| :--- | :--- | :--- |
| [185] | \pi | Pi |
| [183] | \sum | Sum |
| [   | \{ | Open bracket |
| ]   | \} | Close bracket |
| [186] | \int | Integral |
| [178] | \leq | Less than or equal to |
| [179] | \geq | Greater than or equal to |
| [173] | \neq | Not equal to |
| [165] | \bullet | Bullet |
| [201] | \ldots | Horizontal ellipses |
| [215] | \diamond | Diamond |
| [198] | \Delta | Delta |

TeX uses particular fonts for the formulas it produces. These can be overridden in the usual fashion, but the changes are applicable only to letters and digits.

# ## Using Figures in Your Document

Figures that are drawn outside of TeX can be inserted into their own space. This space “floats.” In other words, TeX knows that it must keep track of the figure space as the text around it is added or deleted. This flexibility means that you, the writer, need not worry about exactly where in the document your figures will appear.