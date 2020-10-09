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
    
The output for Dataset 1 can be given by:

![Output for Dataset 1](https://github.com/nimbekarnd/RANSAC-Implementation-Python/blob/main/Output/Dataset1_1.png)

### For Dataset 2

* We can observe that few points (can be termed as outliers) in the this data set are far away from most of the points that are roughly following specific pattern/trend (quadratic curve)
• If we try to fit a curve using just least-square method, the curve might be shifted towards the outliers too in order to reduce the distance between them too and will not be able to describe the data better.
• We can use RANSAC (RANdom SAmple Consensus) algorithm to fit a better curve that can describe the data-set better and also help in detecting/identifying the outliers too.
• Another voting-based algorithm that can be used is Hough Transform. But it RANSAC is applicable for larger number of parameters than Hough Transform and parameters are easier to choose in RANSAC than in the former.
* In RANASC, as the same suggests, we will sample few of the data points in our dataset and try fitting a curve to the sampled data.
    - We count the number of points that whose distance from the line lie within a specific predefined threshold.
    - Iterate again with new sample points , solve for the model, count the inliers and check whether the inlier count is greater than any of the previous ones.
    - We will select the model which had the maximum number of inliers and that will be our solution to P
* To select the model for the sampled data set we used Least-Square model method similar to the way it was done for dataset-1
* Few of the parameters that were chosen for our solution:
    - N = number of iterations : *this was adaptively updated based on number inliers for each model*
    - **N = log(1 - p) / log(1 - (1 - e)<sup>num_samples</sup>)**,  *where **p** = desired probability of the inliers, **e** = probability of the outliers, **num_samples** = number of samples of data we chose for each iteration.*
    - number of sample = 3, minimum three equations are required to get the values of three parameters: *a, b and c* in *ax<sup>2</sup> + bx + c*
    - p = 0.95, so that most of the points can be covered or described by the model
    - e = 1 - inlier_count/total_data_size (it is adaptive)
    - threshold = standard deviation of y/2, having a narrow boundary and checking maximum inliers in it increases the desired overall probability of the inliers.
