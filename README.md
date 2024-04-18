### Optimization of Machine Learning Algorithms through Bayesian optimization and Gaussian Processes

Project for the "Information Theory and Inference" class, held by Prof. Michele Allegra at University of Padova during Academic Year 2023-2024,

by Erica Brisigotti & Ekaterina Chueva

The **goals of the project** are:
- implement a Bayesian Optimization (BO) algorithm from scratch
- test the algorithm on benchmark functions
- apply it to a machine learning task


### Content of the project

#### 1) Bulding a BO algorithm

For the theory the article ["Taking the Human Out of the Loop: A Review of Bayesian Optimization", B. Shahriari, K. Swersky, Z. Wang, R. P. Adams and N. de Freitas, 2016](https://ieeexplore.ieee.org/document/7352306) was taken as a main reference.

The implemeted kernels are squared-exponential, Matern-1, Matern-3 and Matern-5. On top of that, there are two types of acquisition functions: expected improvement and upper confidenc bound ("optimistic"). For the details and context see the jupyter notebook.

#### 2) Testing the algorithm on benchmark functions

Three benchmark functions of different complexity were taken from the [Olympus package](https://aspuru-guzik-group.github.io/olympus/classes/surfaces/index.html): HyperEllipsoid, Levy and AckleyPath. They were taken with the opposite sign, as our algorithm finds maximum of the function.

The results of the testing are provided on the following pictures:

![alt text](https://github.com/EkaterinaChueva/Optimization-of-Machine-Learning-Algorithms-through-Bayesian-optimization-and-Gaussian-Processes/blob/main/HyperEllipsoid.png)

![alt text](https://github.com/EkaterinaChueva/Optimization-of-Machine-Learning-Algorithms-through-Bayesian-optimization-and-Gaussian-Processes/blob/main/Levy.png)

![alt text](https://github.com/EkaterinaChueva/Optimization-of-Machine-Learning-Algorithms-through-Bayesian-optimization-and-Gaussian-Processes/blob/main/AckleyPath.png)

As we can see from the three plots above, there is no single perfect recipe for all functions. 

For Levy and Hyperellipsoid, we notice that:
- the final results are reached by all combinations of policies and kernels, but with varying number of BO iterations
- the optimistic policy starts examining from further points, but is also more likely to change for a better value
- the expected improvement policy starts closer to the final output, but changes less

These tendencies are likely to be related to the smoother shape of the functions.

For AckleyPath, we clearly see from the plots that both policies get stuck in different local maxima, because of the very complicated shape of the function.


#### 3) Applying BO to machine learning

We consider a simple CNN and the MNIST dataset of handwritten digits as our task. The target function is the accuracy of the CNN, while parameters to be optimized are learning rate and the momentum of the stochastic gradient descent.

The results of apllying our algorithm to this task are presented on the following plot:

![alt text](https://github.com/EkaterinaChueva/Optimization-of-Machine-Learning-Algorithms-through-Bayesian-optimization-and-Gaussian-Processes/blob/main/CNN.png)

We notice from the plot that, for our CNN application, the matern-5 kernel seems to be optimal for both policies.

Besides that, we also compare the results obtained with Bayesian optimization with similar packages tools:
- [Keras Tuner](https://keras.io/keras_tuner/) provides multiple algorithm choices, including a Bayesian Optimization one.

- the [Bayesian optimization package](https://github.com/bayesian-optimization/BayesianOptimization)
  
As we found, our implementation is comparable in terms of speed and results with these tools.
