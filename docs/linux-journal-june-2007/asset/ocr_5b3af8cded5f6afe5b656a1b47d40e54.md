to the attr_accessor method in order to create the read/write access methods for all the declared attributes.

Here's how we can use the attr_initialize method:

```
class Student
  attr_initialize :name, :id, :address
end
```

```
s = Student.new('Erika', 123, '13 Fake St')
s.address = '13 Wrong Rd'
puts s.name, s.id, s.address
```

The expected output would be:

```
Erika
123
13 Wrong Rd
```

# Conclusion

Once you're familiar with the techniques, metaprogramming is not as complicated as it might sound initially. Metaprogramming allows you to automate error-prone or repetitive programming tasks. You can use it to pre-generate data tables, to generate boilerplate code automatically that can't be abstracted into a function, or even to test your ingenuity on writing self-replicating code.

Ariel Ortiz is a faculty member at the Computer Science Department of the Tecnologico de Monterrey, Campus Estado de Mexico. He's been teaching computer programming for almost two decades. He's not too sure what his favorite programming language is, but he thinks it's either Scheme, Python or Ruby. He can be reached at ariel.ortiz@itesm.mx.

> "I'd rather write programs that write programs than write programs." —Richard Sites

# Resources

The Jargon File: www.catb.org/esr/jargon

Ruby Cookbook by Lucas Carlson and Leonard Richardson, published by O'Reilly Media, 2006. Chapter 10 of this book contains 16 recipes on reflection and metaprogramming using Ruby. Highly recommended.

The Quine Page: www.nyx.net/~gthomps/qquine.htm. This Web page contains quines in many different programming languages. It even has quines that work in more than one language.

![](bbox=[0.03, 0.53, 0.15, 0.65])

# Expert Included.

Paul has years of experience in matching customers with the servers they need.
What he likes best are servers that combine outstanding performance with long-term value. Paul is impressed by the Rackform ct5vry A411 because it's a compute cluster in one rack unit, with four Dual-Core AMD Opteron 8000 Series processors and 16 DDR2 DIMM sockets.

And he knows that Second-Generation AMD Opteron processors are designed to offer seamless upgradability to Quad-Core, while AMD's Direct Connect Architecture ensures that all eight cores will work together with maximum efficiency right now.

When you partner with Silcon Mechanics, you get more than a powerful AMD server—you get an expert like Paul.

![](bbox=[0.54, 0.52, 1.0, 0.97])

![](bbox=[0.17, 0.84, 0.33, 0.91])

# SILICON MECHANICS

visit us at www.siliconmechanics.com
or call us toll-free at 866-352-1173