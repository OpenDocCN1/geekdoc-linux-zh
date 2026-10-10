# Plane 0:

```
$ a_{0,0,0} $   $\cdots$   $ a_{0,n-1,0} $
$ a_{1,0,0} $   $\cdots$   $ a_{1,n-1,0} $
$\vdots$           $\vdots$
$ a_{m-1,0,0} $   $\cdots$   $ a_{m-1,n-1,0} $
```

# Plane 1:

```
$ a_{0,0,1} $   $\cdots$   $ a_{0,n-1,1} $
$ a_{1,0,1} $   $\cdots$   $ a_{1,n-1,1} $
$\vdots$           $\vdots$
$ a_{m-1,0,1} $   $\cdots$   $ a_{m-1,n-1,1} $
$\vdots$
$\vdots$
```

# Plane ($ p - 1 $):

```
$ a_{0,0,p-1} $   $\cdots$   $ a_{0,n-1,p-1} $
$ a_{1,0,p-1} $   $\cdots$   $ a_{1,n-1,p-1} $
$\vdots$           $\vdots$
$ a_{m-1,0,p-1} $   $\cdots$   $ a_{m-1,n-1,p-1} $
```

# In Storage

Each block of elements in a three-dimensional sequence is stored successively in an array. The stride for the third dimension is used to select the elements for each successive block of elements in the array. The starting point of the three-dimensional sequence is specified as the argument for the sequence in the ESSL calling statement. For example, if the three-dimensional sequence is contained in array BIG, declared as Big(1:20,1:30,1:10), and starts at the second element in the first dimension, the third element in the second dimension, and the first element in the third dimension of array BIG, you should specify Big(2,3,1) as the argument for the sequence, such as in:

```
CALL SCAF3 (BIG(2,3,1),20,600,3,32,2056,16,20,10,1,1,0.0,AUX,30000)
```

See "How Stride Is Used for Three-Dimensional Sequences" on page 104 for a detailed description of how three-dimensional sequences are stored within arrays using strides.