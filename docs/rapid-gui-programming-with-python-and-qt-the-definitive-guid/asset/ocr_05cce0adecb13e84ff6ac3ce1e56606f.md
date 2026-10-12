Python's sort( ) method and sorted( ) function can take additional arguments. So, for example, we could sort the presidents dictionary by dates.

In addition to the keys( ), values( ), and items( ) methods, dictionaries also provide iterkeys( ), itervalues( ), and iteritems( ) methods. These additional methods can be used just like the plain versions, and they provide better performance. However, they cannot be used to iterate over a dictionary whose keys will change during the iteration.

Just like while loops, we can use break to leave a for loop before the iterations are complete. We can also use continue in both kinds of loop to immediately jump to the next iteration. For example:

```
```python
for x in range(-5, 6):
    if x == 0:
        continue # goes directly to the next iteration
    print 1.0 / x, 
```
```

This will produce output like this: “-0.2 -0.25 -0.33333333333333 -0.5 -1.0 1.0 0.5 0.33333333333 0.25 0.2”. Without the continue, we would eventually attempt division by zero and get an exception.

As mentioned earlier, Python's loops can have an optional else clause that is executed only if the loop completed, that is, the else clause will not be executed if break was called inside the loop. An example will make this clearer; here is an inefficient way of generating a list of primes:

```
```python
primes = [2]
for x in range(2, 50):
    if x % 2:
        for p in primes:
            if x % p == 0:
                break # exits the loop and skips the else
            else:
                primes.append(x)
```
```

When we saw the % operator earlier, it was used with string operands and produced a formatted string as its result. Here, we use the % operator with integer operands, and in this context it performs the modulus (remainder) operation, and produces an integer as its result.

At the end, the primes list is [2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47]. The append( ) method is called only if the iteration over the primes list completes, that is, if x is not divisible by any previous prime.

# ## List Comprehensions and Generators

Producing lists using a for loop in conjunction with range( ) is easy. In addition, Python provides an alternative approach called list comprehensions—these are expressions that generate lists. (Note that this and other advanced sections in