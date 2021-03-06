# Understanding Understanding Neural Nets Forwards and Backwards
**Benjamin S. Knight**, March 5th, 2017

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  My goal in writing this is to, step-by-step, calculation-by-calculation, walk through a single epoch of a simple neural network. Recall that an epoch is defined as one iteration of the model that utilizes the entirety of the avialable training data. While the network itself is relatively simple (only three nodes), our discussion will be anything but. Our first objective is to elaborate in detail a single forward pass of the model. The next task involves a bit of calculus - one pass of backwards propagation and the derivation of a gradient from which we calculate a new array of weights for the network. Later on, we will delve into what exactly we mean by a 'gradient,' and how it is calculated. However, before anything else, we need an example model - so let's create one now.  

### One Forward Pass Across a 'Simple' Neural Network

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Our hypothetical network has two input variables 'X1' and 'X2', one output variable 'Y', and a training data set that is comprised of a single observation [8, -4]. The interior of the network is comprised of two layers - one hidden layer of two nodes followed by a single node output layer. We can unpack this network further by visualizing the weights as grey squares. Lastly, the activation function that preceeds the output 'Y' is a sigmoid function.  

<p align="center"><b>Figure 1: An Example Neural Net</b></p>
<p align="center">
<img src="https://github.com/b-knight/Understanding-Error-Signal-Propagation-Forwards-and-Backwards/raw/master/Images_and_GIFs/Establishing_Model_Gif.gif" alt="A GIF showing the construction of a 2-inputs, 1-output, 3-node neural net with a sigmoid activation function in the output layer." width="80%" height="80%">
</p>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; When initializing a neural net, the weights are typically initialized to small random values chosen from a zero-mean Gaussian distribution with a standard deviation of about 0.01 ([Hinton](http://www.csri.utoronto.ca/~hinton/absps/guideTR.pdf), 2010, p.9). We start the forward pass by multiplying our initial inputs ('X1' and 'X2') times their respective weights, and then summing the results. Next, we repeat the process for the nodes in the hidden layer - multiplying the output of H1 times its weight, multiplying the output of H2 times its weight, and summing the two products to create the value associated with the output node 'O1'. Our final step is the activation function - in this case, a sigmoid function.  

<p align="center"><b>Figure 2: Randomly Assigning Weights and Executing the Forward Pass</b></p>
<p align="center">
<img src="https://github.com/b-knight/Understanding-Error-Signal-Propagation-Forwards-and-Backwards/raw/master/Images_and_GIFs/Forward_Pass_GIF.gif" alt="A GIF showing one forward pass of the neural network." width="70%" height="68%">
</p>
<br>

### What is a Gradient?
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; The purpose of backwards propagation is to enable us to train the model - typically with some version of gradient descent. To understand how gradient descent is accomplished, it is helpful to know what a gradient is. Below is a visualization of what an error gradient would look like with two variables. In deriving the error gradient, our variables are referred to as 'edges' - the connections between nodes.

<p align="center"><b>Figure 2: A Three Dimensional Visualization of Gradient Descent</b></p>
<p align="center">
<img src="https://github.com/b-knight/Understanding-Error-Signal-Propagation-Forwards-and-Backwards/raw/master/Images_and_GIFs/Gradient.png" alt="A Three Dimensional Visualization of Gradient Descent Courtesy of Zoran Vrhovski.">
</p>
<p align="center">Source: <a href="https://www.youtube.com/watch?v=wobhkK0h1wc">Zoran Vrhovski</a> May 29th, 2012</p>
<br>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; A neural net can be thought of as one, very large differentiable equation with many variables. To better understand any complex system with many inputs, it is often useful to specify a relationship between the outcome variable and a specific variable of interest. Mathmatically, we do this by taking the partial derivative of the equation with respect to the variable of interest. When taking the partial derivative, any component of the expression that is not somehow associated with the variable of interest is effectively set to zero. Note in the figure below how different elements drop out of relevance based on what variable we are taking the partial derivative with respect to.



For those wanting additional detail, I highly recommend [this](https://www.khanacademy.org/math/multivariable-calculus/multivariable-derivatives/gradient-and-directional-derivatives/v/gradient) series of video lectures from Kahn Academy. 

### Calculating the Gradient


<p align="center"><b>Figure 3: Identifying the Error Derivatives from the Neural Net's Edges</b></p>
<p align="center">
<img src="https://github.com/b-knight/Understanding-Error-Signal-Propagation-Forwards-and-Backwards/raw/master/Images_and_GIFs/Gradient.gif" alt="A Three Dimensional Visualization of Gradient Descent Courtesy of Zoran Vrhovski.">
</p>
<br>



<p align="center"><b> Expression 3: Gradient (Edge 1) - The Loss Function Error</b></p>
<p align="center">
<img src="https://github.com/b-knight/Understanding-Error-Signal-Propagation-Forwards-and-Backwards/raw/master/Images_and_GIFs/Gradient_1.png" alt="Calculating the error of the loss function - here the sum of squares." width="45%" height="45%">
</p>

<p align="center"><b> Expression 4: Gradient (Edge 2) - The Sigmoid (Activation) Function Error</b></p>
<p align="center">
<img src="https://github.com/b-knight/Understanding-Error-Signal-Propagation-Forwards-and-Backwards/raw/master/Images_and_GIFs/Gradient_2.png" alt="Calculating the error of the activation function - here a sigmoid function." width="60%" height="60%">
</p>

<p align="center"><b> Expressions 5 &amp; 6: Gradient (Edges 3-4) - The Output Layer Error</b></p>
<p align="center">
<img src="https://github.com/b-knight/Understanding-Error-Signal-Propagation-Forwards-and-Backwards/raw/master/Images_and_GIFs/Gradient_Output_Layer.png" alt="Calculating the error of the two edges within the output layer." width="70%" height="70%">
</p>

<p align="center"><b> Expressions 7-10: Gradient (Edges 5-8) - The Hidden Layer Error</b></p>
<p align="center">
<img src="https://github.com/b-knight/Understanding-Error-Signal-Propagation-Forwards-and-Backwards/raw/master/Images_and_GIFs/Gradient_Hidden_Layer.png" alt="Calculating the error of the two edges within the output layer." width="70%" height="70%">
</p>
<br>

## References

- Hinton, Geoffrey. [Artificial Intelligence Courses]. (2013, November 4th). *The Backpropagation Algorithm*. Retrieved from [https://www.youtube.com/watch?v=xfPz92B0rv8](https://www.youtube.com/watch?v=xfPz92B0rv8).

- Hinton, Geoffrey. (2010). A Practical Guide to Training Restricted Boltzmann Machines. Retrieved from [http://www.csri.utoronto.ca/~hinton/absps/guideTR.pdf](http://www.csri.utoronto.ca/~hinton/absps/guideTR.pdf).

- Karpathy, Andrej. [MachineLearner]. (2016, June 14th). *CS231n Lecture 4 - Backpropagation, Neural Networks*. Retrieved from [https://www.youtube.com/watch?v=QWfmCyLEQ8U](https://www.youtube.com/watch?v=QWfmCyLEQ8U).


