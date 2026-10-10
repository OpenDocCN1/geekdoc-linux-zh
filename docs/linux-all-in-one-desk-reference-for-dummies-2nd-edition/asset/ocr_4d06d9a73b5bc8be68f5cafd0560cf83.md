![](bbox=[0.25, 0.14, 0.53, 0.49])

![](bbox=[0.55, 0.14, 0.87, 0.43])

![](bbox=[0.55, 0.45, 0.85, 0.66])

**Figure 2-1:**
Typically, several source files make up a C program.

# ## Declaration versus definition

A *declaration* determines how the program interprets a symbol. A *definition*, on the other hand, actually creates a variable or a function. Definitions cause the compiler to set aside storage for data or code, but declarations do not. For example,

```
int x, y, z;
```

is a definition of three distinct integer variables, but

```
extern int x, y, z;
```

is a declaration, indicating that the three integer variables are defined in another source file.