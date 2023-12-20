---
title: Decoding the straight line equation
description: Algebra is generous; she often gives more than is asked of her — Jean le Rond
date: '2019-03-23T07:36:49.342Z'
categories: ["machine learning", "tech"]
keywords: []
slug: /@itsmesunil/decoding-the-straight-line-equation-machine-learning-ba63cf7e4b8
---

![](/img/0__JOQ9EJQpeRlxVibB.jpg)

> Algebra is generous; she often gives more than is asked of her — Jean le Rond

Before getting into Supervised learning branch of machine learning, it is imperative to get an idea about Linear algebra, followed by equation of straight line.

**Linear algebra** is a branch of mathematics which is concerned about linear equations. A linear equation is something which forms a line when drawn and it does have only length property, but no breadth in the mathematical space.

A form of linear equation is shown below:

![](/img/1__Rgwr__Yn9NqaHtRDVolJazw.png)

The term _linear equation represents an equation of first degree._ We can also call the above equation as polynomial ( ‘**poly**’ — many and ‘**nomial**’ — terms) equation. When numbers are added or subtracted to the equation, they are called as terms.

![](/img/1__StBcWu3KuaavOXqBnCiL7A.png)

As we can see in the above picture, the graph of first degree polynomial is always a straight line , the second degree takes the shape of parabola, third degree takes the shape of a curve. Advancing with quartic, quintic polynomials, the equation becomes too complex and graph take different shapes.

The main focus point in this article is to understand that **graph of any first degree polynomial is a straight line** and the straight line equation can be represented as below:

**_y = mx + b_**

Here:

*   y = predicted value or target variable or dependent variable
*   x = independent variable or input or predictor or feature
*   m = slope / weight
*   b = bias / intercept

Here m and b are constants, that defines a linear relationship between x and y. The relationship between x and y is visualized as straight line and hence the term linear.

### Introducing the straight line equation

![](/img/1__6v3__nB3oMXNqFU7SBsCuZw.png)

When **y = x,** we get a straight line which **passes through the origin**. We can inflate **y = x** as below:

**y = 1.x Or**

**y = m.x, where m = 1**

Change in ‘y’ with respect to ‘x’ is represented by

**𝛿y/𝛿x = Slope** ( symbol delta)

When the angle is 45 degrees ( Fig 1 ), **𝛿y/𝛿x = 1 , Since tan 𝚹 of 45 degrees = 1**

The value of **tan⁡(45°)** can be derived exactly by theoretical approach of geometry on the basis of a geometric property. In short ‘**m**’ is the tangent of the angle that the line makes with the X axis.

![](/img/1__6hlAF1iE1ko__8vggjH3g4w.png)

Fig 2 shows different variations of straight line equations, where the value of slope changes depending the angle.

This also represents a straight line, and for all the points on the line, each **y** value is three times the corresponding x value. In all the above cases the line passes through the origin.

Now, look at the second line ( yellow line in [Fig 1](http://Fig%201)) where **y** is not equal to **x.** The line is represented by **y = mx +c,** where c is the intercept. When **c = 0**, the line passed through the origin. The number **c** is the point where the line cuts the **y-axis**.

![](/img/1__cJXvKXl59iBqKMgcYdi2pA.png)

The line is shifted either up or down depending on the value of **‘c’**. If the value of the intercept is positive, the line is shifted up from the origin and vice-verse.

**Conclusion**

Familiarity with linear algebra, before moving into regression algorithms, would help to write custom models in Supervised learning space. The concept of the linear regression is to find a model that represents these points in the best possible way.

Do send me your comments, thoughts to [Sunil Jacob](https://medium.com/u/7d5c1c8a35bd).

**_PS: If you liked the article, please support it with claps. Cheers_**