Line 6 casts an array of Squeezables (s) to an array of Citrus (c). An array is legal if casting the array element is legal (and the element types are references, not primitives). In this example, the question is whether a Squeezable (the element type of array s) can be cast to a Citrus (the element type of the cast array). The previous example showed that this is a legal cast.

# Summary

Primitive values and object references are very different kinds of data. Both can be converted (implicitly) or cast (explicitly). Primitive type changes are caused by assignment conversion, method-call conversion, arithmetic-promotion conversion, or explicit casting.

Primitives can be converted only if the conversion narrows the data. Primitives can be narrowed by casting, as long as neither the old nor the new type is boolean.

Object references can be converted or cast; the rules that govern these activities are extensive because many combinations of cases must be covered. In general, going “up” the inheritance tree can be accomplished implicitly through conversion, going “down” the tree requires explicit casting. Object reference type changes are caused by assignment conversion, method-call conversion, or explicit casting.

# Exam Essentials

Understand when primitive conversion takes place. Assignment and method-call conversion take place when the new type is the same as wider than the old type. Type widths are summarized in Figure 4.3.

Understand when arithmetic promotion takes place. You should know the type of result of unary and binary arithmetic operations performed on operands of any type.

Understand when primitive casting is required. Casting is required when the new data type is neither the same as wider than the old type.

Understand when object reference conversion takes place. The rules are summarized in Figure 4.6. The most common case is when the new type is a parent class of the old type.

Understand when object reference casting is required. The most common case is when the new type inherits from the old type.