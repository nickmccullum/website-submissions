# Polynomial Regression in Python

The hello world of machine learning and computational neural networks usually start with a technique called regression that comes in statistics. Whether you are a seasoned developer or even a mathematician, having been reminded of the overall concept of regression before we move on to polynomial regression would be the ideal approach to take.

## What is regression?
    

We will get ourselves familiar with the concept of regression with a simple example. Let’s say we are looking to buy houses from the same city. Houses of this city are mainly dependent on how many square feet it has. We are concerned with the price and therefore, we need to know whether we are paying the best price for the house we are going to be purchasing. We have the house pricing information with us from one of our friendly realtors. What we are going to do is find a connection between the square feet and the price of the house, so that we can determine whether we are buying the right property. Let’s look at the data.
```python
sqr_feet = [1350, 1472, 1548, 1993, 1998, 2100, 2450]
price = [643000, 679000, 702500, 759000, 760000, 795000, 855000]
```
  

Each of the data in these lists, correspond to the same elements at the same index. We can plot these values using Matplotlib to get an idea about how they look like.
```python
import matplotlib.pyplot as plt
fig=plt.figure()
axes=fig.add_axes([0,0,1,1])
axes.scatter(sqr_feet, price, color='r')
plt.ylabel('Price(USD)')
plt.xlabel('Area(sqft)')
plt.show()
```
  

![](https://lh3.googleusercontent.com/QQqFxri7koXuyjhuzBx7wqHt6edUGURhG4H7woGh86ELg6zCnMRFDDahbLYP-EPjyYLet7QKl6YGBLbxegg8MfvN3VTZR1L26J6tRy9Af8vi8cR0-ec5G309n7Sdct653XD0Yqc)

This is a scatter plot. However, we can also connect the lines to get a better idea on how the points have been distributed.
```python
plt.plot(sqr_feet, price)
plt.ylabel('Price(USD)')
plt.xlabel('Area(sqft)')
plt.show()
```
  

Output:

![](https://lh5.googleusercontent.com/mXoTjdUjqRNDBAUuBerZ-tMguENDC1s-Vjl1Kqu0GD2i1nZLfCv5raCpOPEVjJzWwzlrQVajbkezy3vTteAcLb0HwcQmFicwoBRNw7qNbMmGZPNj5k_eebKLR268D6nCrcp-5DM)

We can see that the price has been increased proportionally with the available floor area of the house. Therefore, we can now come up with an equation to calculate a ballpark value. That way, if we are given a new house and its floor area, we can see whether we are paying a reasonable amount of not. Since this looks like it can be modeled using a straight-line, we can choose an equation after y = mx + c. However, it is not that easy as there are so many straight-lines that can take the shape of this curve. This is where regression comes in.

Regression can be used to statistically determine the gradient and the intercept of the potential straight-line using methods such as the least-squares method that is based on finding the minimum sum of the square residuals. The general idea is that we can use regression to determine the relationship between one dependent and one or more independent variables. In the data science jargon, the dependent variable is also known as y and the independent variables are known as x1, x2, … xi.

Let us use regression and find gradient (m) and intercept (c) for the above example.

We will use the Scikit-Learn module for this. Install it using pip as follows.

`pip install scikit-learn`

  

Now we are set to go. Let’s code.

Let’s first convert our data to float as they are integer values now. Usually, when we are training machine learning models, it is always good to have them as floating point values.
```python
for i in  range(0,len(sqr_feet)):
	sqr_feet[i] = float(sqr_feet[i])
for i in  range(0,len(price)):
	price[i] = float(price[i])
```
  

Let’s confirm that they are floats.

`sqr_feet`

Output:

> [1350.0, 1472.0, 1548.0, 1993.0, 1998.0, 2100.0, 2450.0]

  

Let’s check for the other list as well.

`price`

Output:

> [643000.0, 679000.0, 702500.0, 759000.0, 760000.0, 795000.0, 855000.0]

  

Now we have to reshape our list since they depict a single feature of our dataset. We will use NumPy library for this.
```python
import numpy as np
sqr_feet = np.array(sqr_feet)
sqr_feet = sqr_feet.reshape(-1,1)
sqr_feet
```
Output:

> array([[1350.],
> [1472.],
> [1548.],
> [1993.],
> [1998.],
> [2100.],
> [2450.]])

  
```python
price = np.array(price)
price = price.reshape(-1,1)
price
```
Output:

> array([[643000.],
> [679000.],
> [702500.],
> [759000.],
> [760000.],
> [795000.],
> [855000.]])

  

Now we are all set to train our model. Let’s import LinearRegression from the Sklearn module. This is how our regressor object will be created.
```python
from sklearn.linear_model import LinearRegression
```
  

Let’s create a regressor object.

`regressor = LinearRegression()`

  

Feel free to pick any name for the regressor object. Let’s train our model now.

`regressor.fit(sqr_feet, price)`

  

When we are training the regressor model, the dependent variable always comes as the 2nd parameter in the fit function while the first parameter is the independent variable(s).

We are all set now and our model has been trained. Let’s find out the gradient and the intercept.

`regressor.coef_`

  

Output:

> array([[180.64818208]])

  

`.coef_` property returns an array with all the coefficients of all the features we used to train the model. However, as in this scenario, we only have one independent variable. Therefore, we only get one coefficient.

Let’s find out the intercept now.

`regressor.intercept_`

Output:

> array([408735.90301617])

  

Therefore, now we know that our m and c respectively are 180.648… and 408735.903… .

We can write the equation for the straight line as follows.

**y=180.648*x+408735.903
price=180.648*sqr<sub>feet</sub>+408735.903**

Let’s see how our model looks alongside the data we used to train it.
```python
fig=plt.figure()
axes=fig.add_axes([0,0,1,1])
axes.scatter(sqr_feet, price, color='r', label = 'Data')
x = np.linspace(1000,3000,20)
y = 180.648*x + 408735.908
plt.plot(x, y, color ='b', label='Model')
plt.ylabel('Price(USD)')
plt.xlabel('Area(sqft)')
plt.show()
```
![](https://lh3.googleusercontent.com/NSD1kQxt1qyXBOnHszsNSeBscRYqp2MpZ50rZF3KFZ8rkZ5Pldynwa0aMjc_c-iPkEDOoI2C5IUFNXrp8QKjWYkwxa5Zmq6akys2Dwx6IAOh87AD2ZZaEEOYV6-i6WLxPOQfz50)

  

Let’s make a prediction using the model. Assume that we are presented with a new house from the same region. It has a total area of 1800sqft. We are told a price of USD 790,000.00. We can use the model to see if the price is fair or not.
```python
new_house_sqft = 1800.0
new_house_sqft = np.array([new_house_sqft]).reshape(-1,1)
regressor.predict(new_house_sqft)
```
  

Output:

> array([[733902.63076741]])

Our model says that the property is only worth about USD 733,902. Therefore, we can agree that the advertised price is a bit of an overestimation. That is the basic concept of regression and how we can apply regression in real life.

We will now get on with the topic for the day, polynomial regression.

  

## Polynomial Regression
    

As opposed to linear regression, polynomial regression is used to model relationships between features and the dependent variable that are not linear. In such instances, we cannot use y=mx+c based linear regression to model our data. Instead, we have to go for models of higher orders. These models can be modeled using polynomial equations such as,

**y=a<sub>n</sub>x<sup>n</sup> + a<sub>n-1</sub>x<sup>n-1</sup>+ a<sub>n-2</sub>x<sup>n-2</sup>+ a<sub>n-3</sub>x<sup>n-3</sup>+ ... + a<sub>0</sub>**

  

For instance, these equations could be like, y=x<sup>3</sup> + 1 or even y=5x<sup>4</sup>+ 4x<sup>3</sup> + 2x<sup>2</sup> +4. In these equations, we call the a<sub>n</sub> terms as weights and a<sub>0</sub> the bias. As the order of the equation increases, the complexity of the model inherently increases as well. Let’s learn polynomial regression with an example.

Assume that we have a dataset for CPUs with different hypothetical clock rates. We are using each processor to execute the same task and we are recording the time for each CPU to process the task. The data are as below.

> clock_rate = [600, 650, 700, 750, 800, 850, 900, 950, 1000, 1050,
> 1100, 1150, 1200, 1250, 1300, 1350, 1400, 1450]
> 
> minutes_to_process = [1700.01, 1400.02, 1100.1, 800.01, 496.25,
> 368.11, 337.35, 308.04, 301.36, 300.0, 298.75, 288.92, 248.95,
> 218.33, 178.73, 120.21, 80.20, 60.1]

  

We can plot these data points in a scatter plot to see how they look like.
```python
fig=plt.figure()
axes=fig.add_axes([0,0,1,1])
axes.scatter(clock_rate, minutes_to_process, color='r')
plt.ylabel('Clock Rate (MHz)')
plt.xlabel('Minutes to Process')
plt.show()
```
Output:

![](https://lh4.googleusercontent.com/IpA7TG9JnpEeE-jjNm-8g1JU1trWW6AGj1zR4igK9uJeDn8EAsSPdUtqj4xzH53YRg5k3MoMu_erMEQPyTJhynvzAbUqZA5XKrXM4fMqd9bY9VUUgiD6REUycsLOkVJ9Zb6R8Cg)

  

If we are to connect these lines and get a plot for the ease of visualization, we can do it as follows.
```python
plt.plot(clock_rate, minutes_to_process)
plt.plot()
plt.ylabel('Clock Rate (MHz)')
plt.xlabel('Minutes to Process')
plt.show()
```
Output:

![](https://lh4.googleusercontent.com/u30EYih3EPDHb_lM5ixjRXfFpMldOZotqma03jZtgSTBcFV6BGCqRJyU_niPS3xs19gNQZ76BTNps6RKKm6Dec4CdMe-S-nVCyN3GcMQ7wXTQgzEfkSeynUbfYYC8G0iAtw0A18)

It is easily discernible that the relationship is not linear. Therefore, we cannot accurately model these data using linear regression. However, let us try to model it using linear regression to see what kind of a line it produces.

  
  

### Linear Regression for Curvilinear Data
    

Since we already know how to perform a linear regression, let’s go ahead and code.
```python
for i in  range(0, len(clock_rate)):
	clock_rate[i] = float(clock_rate[i])

clock_rate = np.array(clock_rate)
clock_rate = clock_rate.reshape(-1, 1)
minutes_to_process = np.array(minutes_to_process)
minutes_to_process = minutes_to_process.reshape(-1, 1)

from sklearn.linear_model import LinearRegression
regressor = LinearRegression()
regressor.fit(clock_rate, minutes_to_process)

fig=plt.figure()
axes=fig.add_axes([0,0,1,1])
axes.scatter(clock_rate, minutes_to_process, color='r', label = 'Data')

x = np.linspace(600,1500, 50)
y = regressor.coef_[0][0]*x + regressor.intercept_[0]
plt.plot(x, y, color ='b', label='Model')
plt.ylabel('Clock Rate (MHz)')
plt.xlabel('Minutes to Process')
plt.show()
```
  

Output:

![](https://lh4.googleusercontent.com/e0U6lgVM8nGmNnTiscncNxAGtaY8N64YNCl8Oe8yKb9yh-78I9j6cmV3qV44qtmwoG1nTKcAR2vjAebp1sv4IfgSbLXgceFghTq3i8o-NuIrYpEcYAHeZcXR3YL1417XZiI-WW0)

  

It is apparent that the model produced by linear regression has not been able to accurately model the dataset by capturing the distinctive features of it. This phenomenon is also known as underfitting. We can find the mean squared error of this model for this particular dataset. We can find this using the mean squared error between the true Y values and predicted Y values.

Since we already have the true values, let us create a list with the predicted Y values.
```python
y_pred = []
for i in  range(600, 1500, 50):
	i = np.array([i]).reshape(-1,1)
	y = regressor.predict(i)
	y_pred.append(y[0][0])
y_pred
```
  

Output:

> [1099.616842105263,
> 1026.4948606811145,
> 953.3728792569658,
> 880.2508978328171,
> 807.1289164086686,
> 734.0069349845201,
> 660.8849535603715,
> 587.762972136223,
> 514.6409907120742,
> 441.51900928792566,
> 368.3970278637771,
> 295.27504643962857,
> 222.15306501548002,
> 149.03108359133125,
> 75.90910216718271,
> 2.7871207430341656,
> -70.33486068111438,
> -143.45684210526315]

  

Let’s create a y_true list using the `minutes_to_process` numpy array.
```python
y_true = minutes_to_process
y_true = y_true.tolist()
```
  

Let’s find the mean squared error.
```python
from sklearn.metrics import mean_squared_error
mean_squared_error(y_true, y_pred)
```
  

Output:

> 61432.823

  

We can acquire the root mean squared error as follows to get a better idea.

`np.sqrt(mean_squared_error(y_true, y_pred))`

  

Output:

> 247.85645732715636

  

This is a really high value compared to the output values. Therefore, it further implies that the linear regression model fails to accurately model the behavior of the dataset.

Let us now try to model the data using polynomial regression.

### Polynomial Regression of Order 2 for Curvilinear Data
    

For starters, it should be understood that the polynomial regression consists of two processes. The first one is polynomial transform and then it is followed by linear regression (Yes, it is linear regression). If we think about it, what really happens is we are building an equation with a higher-order by adding higher degrees to initial variables as new variables. For instance, let us say that our linear model is,

**y=a<sub>1</sub>x + a<sub>0</sub>**

This is equivalent to y = mx + c.

By polynomial transform, what we are doing is adding another variable from a higher degree. For instance, the above equation can be transformed to,

**y=a<sub>2</sub>x<sup>2</sup> + a<sub>1</sub>x + a<sub>0</sub>**

by adding a a<sub>2</sub>x<sup>2</sup> term.

The model we develop based on this form of the equation is polynomial in nature.

Let us take this idea into practice.

We will start from the beginning by reassigning the original dataset to our variable names and preparing them to avoid any confusions.
```python
clock_rate = [600, 650, 700, 750, 800, 850, 900, 950, 1000, 1050, 1100,
1150, 1200, 1250, 1300, 1350, 1400, 1450]

minutes_to_process = [1700.01, 1400.02, 1100.1, 800.01, 496.25, 368.11,337.35, 308.04, 301.36, 300.0, 298.75, 288.92, 248.95,218.33, 178.73, 120.21, 80.20, 60.1]

for i in  range(0, len(clock_rate)):
	clock_rate[i] = float(clock_rate[i])

clock_rate = np.array(clock_rate)
clock_rate = clock_rate.reshape(-1, 1)
minutes_to_process = np.array(minutes_to_process)
minutes_to_process = minutes_to_process.reshape(-1, 1)
```
  
  

Then we will use the PolynomialFeatures class to perform the polynomial transform. Note that we are specifying degree=2 to inform the PolynomialFeatures object that we only require an order of 2 for this model.
```python
from sklearn.preprocessing import PolynomialFeatures
poly_features= PolynomialFeatures(degree=2)
clock_rate_poly = poly_features.fit_transform(clock_rate)
```
  

Then we will create a LinearRegression object and train the model using the polynomial-transformed array.
```python
regressor = LinearRegression()
regressor.fit(clock_rate_poly, minutes_to_process)
```
  

Our model is trained now. Then we will predict the respective values using the polynomial-transformed array to acquire the shape of the model so we can plot it later. We are also creating a list of clock_rate values as x values for us to facilitate the plotting process. Note that we are flattening the numpy arrays by creating a list of the predicted values.
```python
y_poly_pred = regressor.predict(clock_rate_poly)

flatten = lambda  x: [i for j in x for i in j]

y_poly_pred = flatten(y_poly_pred)
x_pred = flatten(clock_rate.tolist())
```
  

We will now prepare the initial data so we can create a scatter plot to compare with the model.
```python
for i in  range(0, len(clock_rate)):
	clock_rate[i] = float(clock_rate[i])

clock_rate = np.array(clock_rate)
clock_rate = clock_rate.reshape(-1, 1)
minutes_to_process = np.array(minutes_to_process)
minutes_to_process = minutes_to_process.reshape(-1, 1)
```
  

Let’s plot both our model and data in the same plot.
```python
plt.scatter(clock_rate, minutes_to_process, color='r', label = 'Data')
plt.plot(x_pred, y_poly_pred, color = 'b', label = 'Model')

plt.ylabel('Clock Rate (MHz)')
plt.xlabel('Minutes to Process')
plt.show()
```
Output:

![](https://lh3.googleusercontent.com/IyfPu2aJbfWd1AffxUAc7V4dCsh3LQFswA4FQuWay7C8JnXu5Z5pq4QiThDYPSbIM4wJOc3il0zQkz8BboEOouQrqqN_lMAmrBx62vj6t3w-l80GKk3mvrzspfwHYfOdSYMdVNk)

  

As we can visually perceive, this newer model fits the data better than our last attempt with pure linear regression.

Let us calculate the root mean squared error for this model.

`np.sqrt(mean_squared_error(flatten(minutes_to_process.tolist()),y_poly_pred))`

  

Output:

> 142.65945359894747

  

Although it is not close to zero, as we can see, the root mean squared error value is lower than when we performed a pure linear regression. This further confirms that the accuracy of the newer model is much higher. However, our model still is at an underfitting stage.

Let’s try to increase the order of our model.

  

### Polynomial Regression of Order 3 for Curvilinear Data
    

As we already have the code for polynomial regression, we can go ahead with the same code by changing the `poly_features` declaration as follows.

`poly_features= PolynomialFeatures(degree=3)`

  

This would give us the following model.

![](https://lh5.googleusercontent.com/6X_qqF_VPzJHdk5oPCTkSXb2EH5-9duiIWfvvSpwY_x5XmVRobDIXrtI5EmD7Z223_xwPIfARuML5RnVOk9WHSmUAOa_22eLckuMIecYP_j5QjOgy1gRLgFqQLrUSkztDkOtMJc)

We can see that this new model coincides with more points and therefore, its underfitting status is slowly fading away. Let’s calculate the root mean squared error.

`np.sqrt(mean_squared_error(flatten(minutes_to_process.tolist()),y_poly_pred))`

  

Output:

> 51.5153661408646

  

The error has further decreased showing that our model’s accuracy is getting better.

Let us perform a few more iterations by increasing the order of the model and tabulate the root mean squared error.

|Order of the Model  |Root Mean Squared Error|
|--|--|
| 1 | 247.85645732715636 |
| 2 | 142.65945359894747 |
| 3 | 51.5153661408646 |
| 4 | 46.303623120889505 |
| 5 | 39.208332989178274 |
| 6 | 32.84020949832818 |
| 7 | 38.730126720255285 |
| 8 | 59.92443555957468 |


We can see a gradual decrease in the error as we increase the order. However, at one point, the error starts to increase again. It should be kept in mind that when we are training models, we should make sure that we train our model amply but never more than what is required. Otherwise, the model will start to exhibit an overfitting nature. This will decrease its ability to generalize itself to suit real-world data that we will be using to make predictions. This is why we should be aware of the phenomenon called bias-variance tradeoff.

## Bias-Variance Tradeoff
    

The bias and variance are two of the most important parameters we should be familiar with. In a simple sense, bias is a notion about the error we are introducing to the predictions due to the model we are choosing to represent the real-world data. Variance is a concept about how much flexibility the model is attempting to have in order to coincide with as many data points as possible.

Linear models are inherently high-bias algorithms suggesting that they will not change their shape abruptly due to one or two data points being out of the natural trajectory of the dataset. However, high variance models such as polynomial models of higher orders, KNN models of higher N values suggest that they are prone to quick changes trying to fit through all the data points.

It is a good practice to ensure that all the models we train are low-bias and low variance. However, as we reduce the bias, the variance increases. As we decrease the variance, the bias increases. This is the bias-variance tradeoff.

## Different Python Libraries for Data Science and Machine Learning
    

In this tutorial, we only used the Sklearn library. However, there are many more machine learning libraries that offer different types of features such as better control and optimization over your machine learning models. The following are a few of the most popular and versatile machine learning libraries and platforms available for Python.

-   Theano   
-   TensorFlow    
-   Keras 
-   PyTorch
    

These libraries can be easily installed and some even offer GPU support depending on your hardware which will lead you to train your models much faster. Feel free to install these within your Python environment and perform the linear and polynomial regressions we did today.

## Conclusion
    

Regression is considered to be the hello world in the machine learning world. We learned the building blocks of regression by going through an example of linear regression. Then we learned about polynomial regression and also about how the errors change as we increase the order of polynomial models. We also learned about the bias-variance tradeoff and the best practices to find suitable machine learning models and train them optimally.
