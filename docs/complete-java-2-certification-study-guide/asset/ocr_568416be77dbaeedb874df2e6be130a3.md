![](bbox=[0.168, 0.118, 0.36, 0.269])

Java provides a full set of operators, most of which are taken from C and C++. However, Java's operators differ in some important aspects from their counterparts in these other languages, and you need to understand how Java's operators behaves. This chapter describes all the operators. Some are described briefly, whereas operators that sometimes cause confusion are described in more detail. You will also learn about the behavior of expressions under conditions of arithmetic overflow. In this chapter, we will first look at the different Java operators. The rest of this chapter examines each of these operators. But before we start, let's consider the general issue of evaluation order.

# Overview of the Java Operators

Java's operators, which are shown in Table 2.1, perform traditional arithmetic and logical operations, as well the object-oriented cast and instanceof operations. They are listed in precedence order, with the highest precedence at the top of the table. Each group has been given a name for reference purposes; that name is shown in the left column of the table. Arithmetic and comparison operators are each split further into two subgroups because they have different levels of precedence. We'll discuss these groupings later.

# TABLE 2.1 Operators in Java, in Descending Order of Precedence

| Category | Operators |
|---|---|
| Unary | ++ - ! ~ (type) |
| Arithmetic | * / % + - |
| Shift | << >> >>> |
| Comparison | < <= >= instanceof == !== |