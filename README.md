# RANSAC-Implementation-Python

## Problem Statement

Two files of 2D data points are provided in the form of CSV files. The data represents measurements of a projectile with different noise levels and is shown
in figure 1. Assuming that the projectile follows the equation of a parabola,

* Find the best method to fit a curve to the given data for each case. You have to plot the data and your best fit curve for each case. Submit your code along with the instructions to run it.
* Briefly explain all the steps of your solution and discuss why your choice of outlier rejection technique is best for that case.

![Dataset 1](https://github.com/nimbekarnd/RANSAC-Implementation-Python/blob/main/Dataset/DataSet_1_Q2.png)


![Dataset 2](https://github.com/nimbekarnd/RANSAC-Implementation-Python/blob/main/Dataset/DataSet_2_Q2.png)

## Solution:

We tried to find the best fit curve for the given datasets by RANSAC and Least square algorithm.

On observing the two data sets we can see that in dataset-1 and dataset-2 the relation between x and y is quadratic with some outliers in dataset-2.

### For Dataset 1

* We can use the Least-Square method to fit a curve to the data-model as the data-points are close to each other giving a quadratic shape to the distribution of x v/s y data.
* As the values of x-column are evenly spaced we can go with Least-Square method only (if there could have been some irregular distribution in the values of x, we could have chosen Total-Least-Square as the basic model to fit the curve, but not in this case)
* Using least-square method to find the solution of P in the the equation AP = Y we get:

    P = (A<sup>T</sup>A)<sup>-1</sup>(A<sup>T</sup>Y)

![Output for Dataset 1](https://github.com/nimbekarnd/RANSAC-Implementation-Python/blob/main/Output/DataSet1_1.png)
