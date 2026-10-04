```
<dt-with expr="namespace(cost=get_cost(SKU))">\nPrice breakdown for SKU <dt-var name="SKU"><br>
Cost: <dt-var name="cost" fmt="dollars-and-cents"><br>
Markup: <dt-var expr="cost * .33" fmt="dollars-and-cents"><br>
Retail Price: <dt-var expr="cost * 1.33" fmt="dollars-and-cents"><br>
</dt-with>
```

Inside the block, the variable cost contains the result returned by the get_cost function. After the final tag, the original namespace stack is restored and the variable cost is no longer defined.

# 4.3.8.1 The only Attribute

The only attribute can be used in the namespace stack of the object specified, allowing you to completely replace the namespace stack inside with the block. For example, in the following listing only the id variable using a form we will output:

```
<dt-with name="REQUEST" only>
<dt-if name="id">
  The id is specified: <dt-var name="id">
  <dt-else>
  No id was specified.
</dt-if>
</dt-with>
```

Because the REQUEST object is at the bottom of the namespace stack, it will be the only object that names acquired from inside the block.

> NOTE The only attribute does not turn off acquisition. Using merely replaces the current namespace stack with that of another object, rather than just adding that object's namespace to the current one. Because of this, the only attribute has limited utility.

# 4.3.9 The let tag

The let tag is another construct for adding variables temporarily to the namespace. It is designed as a shortcut to using the tag with the _namespace() function as above. The let tag is a non-empty tag.

Let's say we wanted to place a new namespace at the top of the stack and then populate it with some variable data. Among other things, the let tag functions as if you were using the let tag and the namespace variable. The two examples below are functionally equivalent:

# Example 1

```
<dt-let cost="get_cost(SKU)">
<dt-var name="cost" fmt="dollars-and-cents">
</dt-let>
```