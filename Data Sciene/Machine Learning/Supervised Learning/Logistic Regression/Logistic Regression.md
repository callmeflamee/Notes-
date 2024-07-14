Sometimes we would have our data arranged in a not so linear way and looking at it it's pretty obvious to say that [[Multiple Linear Regression|Linear Regression]] would not help us in making predictions and that is where Logistic Regression comes into play.

Logistic regression is **a supervised machine learning algorithm widely used for binary classification tasks**, such as identifying whether an email is spam or not and diagnosing diseases by assessing the presence or absence of specific conditions based on patient test results.

Consider the following data;
![[Screenshot from 2024-07-10 20-23-08.png]]
 Looking at out data where we have the tumor size on the x axis and two categorical class on the y axis and we have to create a model that will classify between the 2 stages.
To fit a line on the above data we would need a curved line and we can achieve it by applying logistic regression algorithm like so;

![[Pasted image 20240710203306.png]]

We know to draw such a curved line we would need to take help of the **sigmoid function**;
![[Pasted image 20240710203553.png]]

## Equation
---
we know that the line function will correspond to
$$Z = \vec{w}.\vec{x}+b$$
now substituting the _z_ with the sigmoid function we get,
$$f_{\vec{w},b}(\vec{x})=g(\vec{w}.\vec{x}+b)=\frac{1}{1+e^{-(\vec{w}.\vec{x}+b)}}$$
### Interpretation of Output
---
$$f_{\vec{w},b}=\frac{1}{1+e^{-(\vec{w}.\vec{x}+b)}}$$
_"probability"_ that class is 1

Example:
_"x"_ is *Tumor Size*
_"y"_ is 0 (*Not Malignant*)
    is 1 (*Malignant*)

so if the output of our logistic regression is `0.7`
then it means;
70% chance that _y_ is *1* (*Malignant*)

It is often Mathematically expressed as:
$$f_{\vec{w},b}= P(y=1|\vec{x};\vec{w},b)$$
Which translates to;

Probability that _y_ is *1*,
given input _x_ with parameters *w,b*.

## Loss Function
---
The difference between the loss function and the cost function is; loss function shows how well your model is doing on a single training example and the cost function is the summation of all the losses of every training example meaning all the training examples

In simple words the *Loss Function tells us how we are doing on a particular training example*, while the *cost function tells us how we are doing on the entire training set.*

Therefore the loss function for the linear regression would be;
$$\frac{1}{2}(f_{\vec{w},b}(\vec{X}^{(i)})-y^{(i)})^{2}$$
And would be represented as;
$$L(f_{\vec{w},b}(X^{(i)}),y^{(i)})$$
But of course we won't be able to use the above loss function for logistic regression since that would result into a non convex function having lots of local minima.
![[Pasted image 20240710224454.png]]

So to overcome this we have another loss function for 
$$\begin{align}
L(f_{\vec{w},b}(x^{(i)}),y) = -\log(f_{\vec{w},b}(x^{(i)}),y)\text{ if }y^{(i)}=1 \\
-\log(1-f_{\vec{w},b}(x^{(i)}),y))\text{ if }y^{(i)} = 0
\end{align}$$
## Geometric Intuition of the loss function
---
1. If *y is 1*
The graph for log(f) and -log(f) would look something like this:
![[Pasted image 20240710225646.png]]
Where the point of intersection is at 1.
Since this is a classification algorithm we would only require the two values i.e 0 & 1;

![[Pasted image 20240710225903.png]]
On the left we have the graph of -log(f) of only the point between 0 and 1.
$$\begin{align}
\text{As }f_{\vec{w},b}(x^{(i)})→1 \text{ then loss → 0} \\
\text{As }f_{\vec{w},b}(x^{(i)})→0 \text{ then loss → }\infty
\end{align}$$
If the algorithm predicts a probability close to 1 and the true label is 1, then the loss is very small. It's pretty much 0 because you're very close to the right answer.

Whereas in contrast, if the algorithm were to have outputs at 0.1 if it thinks that there is only a 10 percent chance of the tumor being malignant but y really is 1. If really is malignant, then the loss is this much higher value

So when y=1 the loss function incentivizes or helps push the algorithm to make better predictions because the loss is lowest when it predicts values close to one.

2. If *y is 0*
The graph for -log(1-f) would look something like this;
![[Pasted image 20240710231113.png]]
Here again we would only need to look at the 0 to 1 part since we only need those two values for classification

![[Pasted image 20240710231228.png]]
$$\begin{align}
\text{As }f_{\vec{w},b}(x^{(i)})→0 \text{ then loss → 0} \\
\text{As }f_{\vec{w},b}(x^{(i)})→1 \text{ then loss → }\infty
\end{align}$$
The same story here too.

Therefore in Summary;
*The further the prediction `f` is from the target's `y` true label, the higher the loss*

The reason we use the above mentioned loss function is because that function results into a convex function that has a global minimum.

## Cost Function
---
To write the cost function we would first need to simplify the loss function which can be written as follows;
$$L(f_{\vec{w},b}(x^{(i)}),y^{(i)}) = -y^{(i)}\log(f_{\vec{w},b}(x^{(i)}))-(1-y^{(i)})\log(f_{\vec{w},b}(x^{(i)}))$$
You notice that there are some extra terms such as `y` and also some extra -ve signs, that simply explains the dual nature of the equation like for ex.

1. if *y = 1*
- we substitute the term $y^{(i)}$ as 1 and the second half of the equation gets reduced to 0 we get the above mentioned loss function.
2. if *y = 0*
- we substitute the term $y^{(i)}$ as 0 and the first half of the term is reduced and we are left with the above mentioned loss function.

Now to finally write the cost function for logistic regression we can do so as following;
$$
J(\vec{w},b) = \frac{1}{m}\sum_{i=1}^{m}[L(f_{\vec{w},b}(\vec{x}^{(i)}),y^{(i)})]$$
$$J(\vec{w},b)=-\frac{1}{m}\sum_{i=1}^{m}[y^{(i)}\log(f_{\vec{w},b}(\vec{x}^{(i)}))+(1-y^{(i)})\log(f_{\vec{w},b}(\vec{x}^{(i)}))]
$$

## Gradient Descent
---
The mathematical equation for [[Gradient Descent]] remains the same as it was in Linear Regression.
Repeat {
$$\begin{align}
w_{j}=w_{j}-\alpha\frac{1}{m}\sum_{i=1}^m(f_{(\vec{w},b)}(\vec{x}^{(i)})-y^{(i)})x_{j}^{(i)} \\
b = b-\alpha\frac{1}{m}\sum_{i=1}^{m}(f_{(\vec{w},b)}(\vec{x}^{(i)})-y^{(i)})
\end{align}$$
}simultaneous update
