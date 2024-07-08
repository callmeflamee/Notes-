How linear regression work is that we first input our features in the Learning Algorithm and then the output is passed into the the function (historically called a hypothesis) and the job of this function is to take a new input of X and provide with a prediction or an estimate which we call as "Y<sup>^</sup>" (y-cap)

![[Drawing 2024-06-30 16.31.48.excalidraw]]
### How to represent F?
---
We can represent our Univariate Linear Regression function as follows;

$$
F_{w,b}(X)=WX+b
$$
$$
OR
$$
$$
F(X)= WX +b
$$

where;
W & B are called as the parameters and sometimes as Weights and also Co-efficients![[Screenshot from 2024-07-02 16-54-26.png]]
As we can see by tinkering with the values of w&b we are getting a a straight line, having "w" as slope of the line and "b" as the height.
![[Pasted image 20240702165621.png]]
Now, how do we find the right value of our weights such that
the line drawn is touching or being close to all of the points in our training set? i.e
$$
\widehat{y}^{(i)}\text{ is close to }y^{(i)}\text{ for all }(x^{(i)},y^{(i)})
$$
## Cost Function
---
### Formula
---
The squared error cost function is expressed as:
$$
J(w,b) = \frac{1}{2m}\sum_{i = 1}^{m}(\widehat{y}^{(i)}-y^{(i)})^2
$$
where; m = number of training examples
we first calculate the summation of all the training example's squared error between the estimation and the actual value then find the average by dividing the entire expression by "m" and as a convection we also divide it by 2.

We also know that the term $$\widehat{y}^{(i)} \text{ is equal to }f_{w,b}(x^{(i)})$$
Therefore we can rewrite our cost function as follows:
$$
J(w.b) = \frac{1}{2m}\sum_{i=1}^{m}(f_{w,b}(x^{(i)})-x^{(i)})^2
$$
Eventually we are going to have to find the values of w,b that make the cost function small

### Intuition
---
Let's have a look at the simplified version of the cost function, where we use only one parameter i.e w.
$$f_{w}(x)=wx\text{ where b = }\phi$$
$$
J(w) = \frac{1}{2m}\sum_{i=0}^{m}(f_{w}(x^{(i)})-x^{(i)})^2
$$

And our goal is to $$minimize_{w}\text{ }J(w)$$
consider:
![[Drawing 2024-07-02 20.55.34.excalidraw]]
Let's observe the value of our cost functions with different values of w.

taking w = 1 we get,
![[Drawing 2024-07-02 20.57.28.excalidraw]]
The difference between the estimates value and the target value is 0 since the line drawn is exactly on the point and hence;
$$\frac{1}{2m}(0+0+0)^2=0$$
the value of the cost function at `w = 1` is 0

now taking `w = 0.5` we get,
![[Drawing 2024-07-02 20.58.11.excalidraw]]
solving for the cost function we get,
$$\frac{1}{2*3}((0.5-1)^2+(1-2)^2+(2-3)^3) = \frac{1}{6}\text{ }3.5 = 0.58$$
Therefore the value of cost function J(w) is 0.58

similarly, for `w = 0` we get,
![[Drawing 2024-07-02 20.58.40.excalidraw]]
$$\frac{1}{2m}(1^2+2^2+3^2)=\frac{13}{6}=2.3$$
calculating the same for different values of w and plotting a graph;

![[Pasted image 20240702210108.png]]
As we observe it is forming a parabola. The least value of cost function is obtained when we set the value of w as `w = 1`and that was our goal i.e to minimize the cost function.

Now let's go back to our original equation where we had both the parameters `(w,b)` 

Plotting the function **`f(w,b)`** results into a 3D plot, that looks like a bowl;
![[Pasted image 20240702223603.png]]
As we can see the corners of the graph are really pointy however the center is a really flat and is pushed inside.

That represents the least value of the cost function

To better understand and read the 3D graph we can plot a contour graph, where the eclipses i.e the function have the same value but at different values of the parameter:
![[Pasted image 20240702224036.png]]
Looking at certain points we can see the value of our parameters and the line they draw and can easily tell weather the line is in our favor or not
![[Pasted image 20240702224208.png]]
![[Pasted image 20240702224237.png]]
Here we see that the center most point in the contour plot is actually the least possible value of our cost function and we can also observe the line drawn is in fact the best compared to our last choices.

But how do we go about selecting the right value that provides the least value of to our cost function?
doing it manually is nearly impossible since it has the time complexity of O(infinity).

There actually exist an algorithm whose purpose is to find the least possible value of our cost function which is called as **[[Gradient Descent]]**
