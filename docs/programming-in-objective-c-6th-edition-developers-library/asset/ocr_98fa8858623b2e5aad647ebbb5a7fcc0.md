not as bad: The field can be shifted into the low-order bits of the word and then ANDed with a mask of the appropriate bit length. So, to extract the t          field of p              and assign it to n, the statement

```
n
```

does the trick. 
The C language does provide a more convenient way of dealing with bit fields. This method uses a special syntax in the structure definition that allows you to define a field of bits and assign a name to that field. Whenever the term “bit fields” is applied to C, it is this approach that is referenced. 
To define the bit field assignments previously mentioned, you can define a structure called p              , for example, as follows:

```
s 
{

} 

```

The structure p                   is defined to contain six members. The first member is not named. 
The :   specifies three unnamed bits. The second member, called f  , is also an u              . 
The :   that immediately follows the member name specifies that this member is to be stored in one bit. The flags f   and f   are similarly defined as being a single bit in length. The member t          is defined to occupy eight bits, whereas the member i             is defined as being 18 bits l       . 
This C compiler automatically packs the preceding bit field definitions together. The nice thing about this approach is that the fields of a variable defined to be of type p              can now be referenced in the same convenient way normal structure members are referenced. So, if you declare a variable called p              as follows: 


```
s 

```

you could easily set the t          field of p                  to 7 with the simple statement 


```
p 

```

or you could set this field to the value of n with the similar statement 


```
p 

```

In this last case, you need not worry about whether the value of n is too large to fit into the t field; only the low-order eight bits of n will be assigned to p        . 
Extraction of the value from a bit field is also automatically handled, so the statement 


```
n 

```

extracts the t          field from p                      (automatically shifting it into the low-order bits as required) and assigns it to n.