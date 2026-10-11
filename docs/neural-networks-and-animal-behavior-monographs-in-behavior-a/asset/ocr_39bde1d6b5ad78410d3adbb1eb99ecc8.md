using general-purpose programming languages such as Pascal, C, C++, etc. These have no knowledge of neural networks as such, yet simple neural network simulations can be implemented easily. For instance, to simulate a two-layer network with one output node, one needs simply two arrays of numbers to store the input and weight vectors, one number for the response, as well as the ability to compute weighted sums and define transfer functions. As an example, Listing 2.1 shows a complete C program that calculates the output of a two-layer network with a single output node and weights **W** = (1, 0, 1, 0) to the input **x** = (1, 1, 1, 1). The program would not look too different in most other programming languages. People have also developed additions to the languages, called *libraries*, that allow programming of more complex simulations with little effort. Typically, these libraries provide data structures to represent various network architectures, as well as the ability to perform common tasks such as calculating network responses or gradient descent learning. Exploring such language extensions probably would be rewarding for readers with some programming experience or those who wish to start programming. Many neural network libraries are listed at http://www.faqsg.org/faqs/ai-faq/neural-nets/part5.

Software for scientific computation is well suited for beginners wishing to simulate simple or moderately complex networks using a rather straightforward programming language. The key insight is that the operation of neural networks can be expressed in terms of vector and matrix algebra, for which extensive support exists. In the following we present a few examples in a syntax common to the programs Octave (http://www.octave.org, available free of charge) and Matlab (http://www.mathworks.com). Similar software, although with different programming syntax, are Scilab (http://www.scilab.org, available free of charge) and Mathematica (http://www.wolfram.com). Many of the models in later chapters require only a little more programming than the following examples, and we encourage the reader to try to reproduce some of our results. We do not expect readers without programming experience to understand each line of the code that follows but rather to get a flavor of neural network coding with scientific software.

# ### 2.5.1 Two-layer feedforward networks

Simple neural networks are coded rather compactly in scientific software. For instance, the following code is equivalent to Listing 2.1:

```
```
1 function r = f( y )
2     r = 1 ./ (1+exp(-y)); % cf. equation (2.7)
3 end
4
5 x = [ 0 1 0 1];        % input vector
6 W = [ 1 1 1 1];        % weight vector
7 r = f( W*x )          % cf. equation (2.17)
```
```

Note how the last line translates equation (2.17) almost literally, with $\hat{W} * \hat{x}$ as equivalent to the notation **W** · **x** for a weighted sum. By convention, the result of a computation is printed out if the corresponding line does *not* end with a semicolon; hence the code above will display the value of $r$, i.e., $r = 0.88080$.