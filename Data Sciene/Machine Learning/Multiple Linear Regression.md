### Notations:
---
![[Pasted image 20240707215551.png]]

### Linear Regression Equation
---
![[Pasted image 20240707215723.png]]
Here, w1 having the value of 0.1 could mean that the price increases by 0.1 for every sq.ft,w2 having the value of 4 means that the price increases by 4 for each bedroom, for w3 the price increases by 10 for every floor the house has and decreases by 2 for every year the house has been built and b = 80 i.e the base price meaning that that is the price of a house with nothing.

## Model
---

$$f_{\vec{w},b}(\vec{x})=\vec{w}\text{ . }\vec{x}+b$$
Where;
vector w is the list of parameters
vector x is the list of inputs
and the "." is the dot product of the two vectors
i.e;
$$\vec{w}=[w_{1},w_{2},w_{3},\dots w_{n}]$$
$$\vec{x}=[x_{1},x_{2},x_{3},\dots x_{n}]$$
Therefore;
$$f_{\vec{w},b}\vec{w}.\vec{x}+b = [w_{1}x_{1},w_{2}x_{2},w_{3}x_{3},\dots w_{n}x_{n}]+b$$
## Cost Function
---
$$J(\vec{w},b)$$
## Gradient Descent for Multiple LR
---
Repeat{
$$w_{j}=w_{j}-\alpha\frac{d}{dw_{j}}j(\vec{w},b)$$
$$b=b-\alpha\frac{d}{dw}j(\vec{w},b)$$
Simultaneously update w & b
} until convergence.

And of course solving the derivative term gives us:

$$w_{n} = w_{n}-\alpha\frac{1}{m}\sum_{i=1}^{m}(f_{\vec{w},b}(\vec{X}^{(i)})-Y^{(i)})X_{n}^{(i)}$$
$$b = b-\alpha\frac{1}{m}\sum_{i=1}^{m}(f_{\vec{w},b}(\vec{X}^{(i)})-Y^{(i)})$$
Simultaneously update 
wj (for j = 1,...,n) and b

## Normal Equation
----
![[Pasted image 20240707223835.png]]