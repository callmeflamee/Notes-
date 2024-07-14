Sometimes our machine learning algorithm may run into the problem of fitting i.e the problem of overfitting or underfitting which can cause our algorithm to perform poorly
## What is the problem of Fitting?
---
Let's understand these with the help of an example;

In the case of Regression Algorithm, imagine we have the dataset of housing prices;
![[Screenshot from 2024-07-14 21-33-46.png]]

We see that we have 3 scenarios where we encounter our 2 problems i.e _overfitting_ and _underfitting_.

Let's take a look at each one of the three;
1. **Underfit**:
- When our model has some sort of a bias; The bias here means that the model thinks that the data is linear  when in fact it isn't so it tries to confirm it's bias by drawing a straight line.
2. **Generalization**:
- When our model makes a hasty generalization by appealing to all the points in our dataset to make a generalized prediction; Naturally we consider this as pretty good and this is what we typically aim for. 
3. **Overfit**:
- When our model draws a line that crosses every data point perfectly and to achieve this draws a very curvy and complicated line; The problem with overfitting is that it tires to mimic perfectness but looses it's predictability on new data points which are unique to the training set.

For classification we have the same story.
![[Pasted image 20240714213807.png]]

## Addressing OverFitting:
---
We have **3** options which one can take to minimize the over or under fitting problems those are:
1.**Gathering More Data:**
- If one can gather more data and then again feed it into the training set then train the model again it is often observed that the model fits the data well since it has now additional options; for example:
![[Pasted image 20240714220257.png]]
2. **Feature Selection:**
- Selecting or excluding some features to feed into your model may help the algorithm to choose a better line that fits your data in a more generalized way, tho it has some downsides if the domain you're working on is unfamiliar to you, you might loose on some useful features.
3. **Regularization:**
- Instead of eliminating some features i.e setting their value to zero, we can minimize the values of some of the $w_{j}$ features; $w_{j}\approx0$ Changing the value of the parameter $b$ is not seen as something useful or either harmful, it's convection to regularize only the parameter $w_{j}$.
![[Pasted image 20240714220801.png]]

## Regularized Linear Regression:
---
### The cost function:
---
$$J(\vec{w},b) = \frac{1}{2m}\sum_{i=1}^{m}(f(\vec{w},b)(\vec{x}^{(i)})-y^{(i)})^2+\frac{\lambda}{2m}\sum_{j=1}^{n}w_{j}^{2}$$
where;
$\lambda = \text{Regularization parameter}$
$n=\text{no of features}$

And dividing the $\lambda$ by $2m$ is a convection; so that both the fist and the second term are scaled by $\frac{1}{2m}$

The goal here is to obviously minimize both the terms; minimizing the first term i.e the mean squared error will help fit the data and minimizing the second term i.e the regularization term will help reduce overfitting. 

The value of lambda that you choose, specifies the relative importance or the relative trade off or how you balance between these two goals.

### Implementing Gradient Descent:
---
$$\begin{align}
w_{j} = w_{j}-\alpha\frac{1}{m}\sum_{i=1}^{m}(f_{\vec{w},b}(\vec{x}^{(i)})-y^{(i)})x_{j}^{(i)}+\frac{\lambda}{m}w_{j} \\
b = b -\alpha \frac{1}{2m}\sum_{i=1}^{m}(f_{\vec{w},b}(x^{(i)})-y^{(i)})
\end{align}$$

## Regularized Logistic Regression

---
### Cost Function:
---
$$J(\vec{w},b)=-\frac{1}{m}\sum_{i=1}^{m}[y^{(i)}\log(f_{\vec{w},b}(\vec{x}^{(i)}))+(1-y^{(i)})\log(f_{\vec{w},b}(\vec{x}^{(i)}))]+\frac{\lambda}{2m}\sum_{j=1}^{n}w_{j}^{2}$$

### Implementing Gradient Descent:
---
$$\begin{align}
w_{j} = w_{j}-\alpha\frac{1}{m}\sum_{i=1}^{m}(f_{\vec{w},b}(\vec{x}^{(i)})-y^{(i)})x_{j}^{(i)}+\frac{\lambda}{m}w_{j} \\
b = b -\alpha \frac{1}{2m}\sum_{i=1}^{m}(f_{\vec{w},b}(x^{(i)})-y^{(i)})
\end{align}$$
