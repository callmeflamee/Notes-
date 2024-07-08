
### Definition
**Machine Learning :** A field of study that gives the computer the ability to learn something without being explicitly programmed

**Well posed learning problem :** A computer program is said to learn from experience E with respect to some task T and some performance measure P
If its performance on T measured by P improves with experience E.

## Supervised Learning:
In this type of ML we are given 2 labelled data(s) X and Y and we have to figure out a relationship between then, i.e finding the the mapping between x and y

for example let's say we have the housing price data were we are given two labelled data, first one is the size of the house in sq. foot and another we have the price of such houses and our job is to find a relationship between the area of the house and the price of the house. We have to make observations such as whenever 'X' is increasing/decreasing what is happening to 'Y', in short we have to find the proportionality between the two labels
![[Pasted image 20240629172628.png]]
We make use of Supervised learning to predict things, as to if we input a certain value of 'X' which is unique to the data at hand into the **Linear Regression** model  and what is the type of output we receive?

### Linear Regression :
It is a type of algorithm that analyses the data and draws a straight line on the graph in such a way that most of the points on the graph are on the line drawn
This line is considered as the best denominator if we were to predict the outcomes in the future.

### Classification :
Within the category of Supervised machine learning we have one more type of problem which are known as the classification problems.

Let's take the example of a patient having a tumor in his brain and we have a labelled dataset that shows the a correlation between the tumor size and weather it is benign or malignant
![[Pasted image 20240629172920.png]]
In such a problem we don't have any quantitative assessment of the parameters and hence we can't really use Linear Regression here.
So we have to use another algorithm called as **Logistic Regression**.

### Logistic Regression:
Consider the below example where we have 3 labels Age which is on y axis, Tumor Size which is on X axis and the two category plotted as points where 'X' denotes malignant and '0' denotes benign

What logistic regression does is that it draws a straight line in the dividing area meaning on one side it will contain most of the 'X' points and "0" on the other side.
![[Pasted image 20240629173141.png]]
There is a problem here that in the real world we will obviously have more than 3 data labels to determine the condition of the tumor but we cant really plot more than 3 data labels on the graph and hence we have to use a different method if we ever encounter more than 3 data labels and that is **Support Vector Machine**, this allows you to store infinite dimensions of vectors

## Machine Learning Strategy (Learning Theory)
It is a way or an insight that we make after looking at our data and deciding what type of machine learning algorithm will be the best suited for our dataset and hence make better and more efficient models

## Reinforcement Learning :
It is the process of making the computer learn on its own by using the reward/punish method, meaning if the AI/model makes a mistake we call it bad and then the machine takes that into account and avoids making that particular move and we reward it if it does something that suits our agenda