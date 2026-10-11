the \`[^]\` character, copy the string into place, and update the pointer. Similar functions existed for formatting and displaying the other kinds of flags in the program.

The code is both repetitive and error prone, and for *gawk* 3.1 we were able to simplify and generalize it. Here's how *gawk* now does it. Starting with this definition in *awk.h*:

```
/\* for debugging purposes \*/  
struct flagtab {  
	int val;                     _Integer flag value_  
	const char \*name;          _String name_  
};
```

This structure can be used to represent any set of flags with their corresponding string values. Each different group of flags has a corresponding function that returns a printable representation of the flags that are currently set. From *eval.c*:

```
/\* flags2str \--- make a flags value readable \*/  
  
const char \*  
flags2str(int flagval)  
{  
	static const struct flagtab values\[\] = {  
	 {  MALLOC,  "MALLOC"  },  
	 {  TEMP,   "TEMP"   },  
	 {  PERM,   "PERM"   },  
	 {  STRING, "STRING" },  
	 {  STRCUR, "STRCUR" },  
	 {  NUMCUR, "NUMCUR" },  
	 {  NUMBER, "NUMBER" },  
	 {  MAYBE\_NUM, "MAYBE\_NUM" },  
	 {  ARRAYMAXED, "ARRAYMAXED" },  
	 {  FUNC,   "FUNC"   },  
	 {  FIELD,  "FIELD"  },  
	 {  INFLSTR, "INFLSTR" },  
	 {  0,   NULL  },  
};  
	return genflags2str(flagval, values);  
}
```

flags2str() defines an array that maps flag values to strings. By convention, a 0 flag value indicates the end of the array. The code calls genflags2str() (“general flags to string”) to do the work. genflags2str() is a general-purpose routine that converts a flag value into a string. From *eval.c*: