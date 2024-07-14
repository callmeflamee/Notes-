It is **one of the most important** machine learning algorithm that is used widely in Machine Learning, and even in training Neural Networks and also Deep Learning.

The purpose of Gradient Descent is to minimize your cost function. 

The outline:
1. Start by some value of w,b
2. Keep changing w,b to minimize f(w,b)
3. until we settle at or near a minimum

It is not necessary that every time the graph will be of a parabola or a hammock shape so it is possible that there may exist more than one minimum.

### How does Gradient Descent work?
---
Consider the following 3d plot, here this is not a squared error cost function and hence it is not a bowl or hammock shape, this is the cost function of a neural network;

![[Drawing 2024-07-06 15.45.50.excalidraw]]

Now imagine that you were standing on top of any one of the hill and then you turn around 360 and decide whats the quickest way downhill then proceed to take a baby step in the direction you choose, now you're at another point and again you turn 360 degrees, look around then take another baby step, now we keep repeating the steps till we are at the bottom i.e the minimum point.

![[Screenshot from 2024-06-30 17-23-44 1.png]]

But what if you choose another starting point a little to the right to that of your previous start point and again you follow the same steps to descend the hill and again you have found another bottom i.e another minimum. 

![[Screenshot from 2024-06-30 17-24-31.png]]

These two points are called as the local minima.

![[Pasted image 20240706154354.png]]

### Implementing Gradient Descent
---
We assign two variables and keep updating the values of the parameters w&b.
$$w=w-\alpha\frac{d}{dw}j(w,b)$$
$$b=b-\alpha\frac{d}{dw}j(w,b)$$
where, 
alpha is the learning rate, it controls the size of our step;
the derivative term decides the direction;
and the entire term is assigned to w&b.

---
We repeat the above steps i.e updating the parameters value until convergence i.e when the value of J(w,b) comes to a local minima and changing the value of parameters beyond this point results in negligible change in the cost function's value.

The correct way to implement this is shown below:
$$tempw=w-\alpha\frac{d}{dw}j(w,b)$$
$$tempb=b-\alpha\frac{d}{dw}j(w,b)$$
$$w=tempw$$
$$b = tempb$$
where the value of the parameters are to be updated simultaneously.

---
### Learning Rate
---
The choice of the learning rate, alpha will have a huge impact on the efficiency of your implementation of gradient descent. 
And if alpha,the learning rate is chosen poorly rate of descent may not even work at all.

If the learning rate is chosen poorly for example if
1. if alpha is too small then:
	1. Gradient Descent may be slow.

2. if alpha is too large then:
	1. Gradient descent may overshoot, may never reach local minimum.
	2. Fail to converge and may even diverge.

As the slope of the line gets flatter the gradient descent algorithm will take smaller and smaller steps until the slope has flatten out i.e the slope of 0 in that case the algorithm will stop.

Meaning when near a local minimum:
- Derivative becomes smaller.
- Update steps become smaller.
Therefore we can reach local minimum without having to decrease the learning rate alpha.

### Gradient Descent Algorithm
---
We had previously written the mathematical equation of Gradient Descent and that was:
$$w=w-\alpha\frac{d}{dw}j(w,b)$$
Upon solving the derivative term we get,
$$w=w-\alpha\frac{1}{m}\sum_{i=0}^m(f_{(w,b)}(x^{(i)})-y^{(i)})x^{(i)}$$
And we repeat the above until convergence.

#### Running the Gradient Descent:
---
![[Pasted image 20240706165230.png]]
As we see in the above image we apply the algorithm to our housing data set and we found the minima by taking small baby steps.

This type of  model use is called as the "Batch" Gradient Descent.

"Batch" : Each step of gradient descent uses all of the training examples.
