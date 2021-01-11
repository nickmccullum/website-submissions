## Introduction

Python provides a number of data structures for data storage. 

NumPy arrays and Pandas Series are common data storage structures among Python programmers when doing data analysis tasks.  

Oftentimes, programmers find it difficult to choose between the two data structures. 

Although the two can be used for storage of similar types of data, they exhibit different performance characteristics. 

In this article, I will do a performance comparison between NumPy arrays and Pandas Series. 

## What are NumPy Arrays?

A numpy array is a grid of values that belong to a similar data type. 

The numpy array values are indexed by a tuple of nonnegative integers. 

The number of dimensions of the array denote its *rank*, while the size of the array along each dimension denote its *shape*. 

The array object in numpy is known as *ndarray*.

To create a numpy ndarray object, you can use the `array()` function. 

For example:

```
import numpy as np

arr = np.array([0, 1, 2, 3, 4])

print(arr)

```

We begun by importing the numpy library. 

We then called the `array()` function to generate an array named `arr` with 5 integer elements. 

The code should return the following array:

![](Capture1.png)

You can also create an ndarray object by passing any array-like object such as a list or a tuple into the `array()` function. 

The `array()` function will convert the object into an array. 

For example:

```
import numpy as np

x = np.array((0, 10, 20, 30, 40))

print(x)

print(type(x))

```

We have passed a tuple with 5 integer elements to the `array()` function. 

The `type()` function should return the object class to which `x` belongs. 

The code should return the following array:

![](Capture2.png)

The values of an array are accessed using indices and the square bracket notation, with the first value being at index 0 and the last value being at index *n-1*, where n is the size of the array. 

For example, to access the third element of the above array, we can use the following code:

```
x[2]
```

The code returns the following:

![](Capture5.png)


## What is a Pandas Series?

The Pandas Series is a one-dimensional labeled array that can hold data of any type. 

Collectively, the axis labels are known as the *index*. 

See the Pandas Series as a column in an Excel sheet. 

The labels must be unique and of a hashable type. 

The Pandas Series supports both integer and label-based indexing and comes with numerous methods for performing operations involving the index. 

There are different ways through which you can create a Pandas Series, including from an array. 

To create a Pandas Series from a numpy array, simply pass the name of the numpy array to the `Series()` function of the Pandas library. 

For example:

```
import pandas as pd
 
import numpy as np
 
# a numpy array
arr = np.array(['a','c','k','l','q'])
 
ser = pd.Series(arr)
print(ser)
```

In the above code, we begun by creating a numpy array named `arr` with a number of character values. 

We then passed the name of this array to the `Series()` function of the Pandas library to convert it into a Series. 

The code returns the following Series object:

![](Capture3.png)

The Series returns index-value pairs, with the indices identifying the Series elements.

The values of the Series object are just a familiar numpy array which can be accessed using the `.value` attribute:

```
ser.values
```

![](Capture3.png)

The specific Series elements can be accessed by their corresponding index via the Python's square-bracket notation. 

For example, you can use the following code to access the element located at index 3 of the Series:

```
ser[3]
```

The code should return the following:

![](Capture6.png)

You can also access the Series elements as a range:

```
ser[1:4]
```

The code should return the Series elements from index 1 to 3:

![](Capture7.png)

You will later see that the Pandas Series is much more flexible and general than the one-dimensional numpy array. 

In the next few sections, we will be discussing how the two, that is, numpy arrays and Pandas Series compare in terms of performance. 

## Performance Comparison between NumPy Arrays and Pandas Series

### Pandas Series as a Generalized NumPy Array

From what we've discussed above, you may think that the Pandas Series is interchangeable with the one-dimensional numpy array. 

The main difference is the index. 

The numpy array has an implicitly defined integer index used to access the values, while the Pandas Series has explicitly defined index associated with the values. 

The explicit index definition of the Series object gives it additional capabilities. 

For instance, the indices must not be of an integer type, but of any desired type. 

For example, you can use strings as the index:

```
ser = pd.Series([0.5, 0.75, 1.0, 1.25],
                 index=['a', 'b', 'c', 'd'])
ser
```

The code should run as follows:

![](Capture8.png)

The index values are now of string data type. 

And the values can be accessed as follows:

```
ser['c']
```

![](Capture9.png)

You can even use non-sequential or non-contiguous indices:

```
ser = pd.Series([0.5, 0.75, 1.0, 1.25],
                 index=[2, 5, 8, 1])
ser
```

![](Capture10.png)

This is impossible with a numpy array, where the indexes must be of an integer data type, must be sequential, and the first element of the array is always at index 0. 

### Operations between Series objects automatically align data based on the label

It is more efficient to align data and match labels with Series objects than with ndarrays. 

A good example is when you're dealing with missing values. 

If there are no matching labels during alignment, Pandas will return *NaN* instead of any number so that the operation doesn't fail. 

For example:

```
ser1 = pd.Series([0.5, 0.75, 1.0, 1.25],
                 index=[2, 5, 8, 1])
ser2 = pd.Series([0.25, 0.5, 1.0, 1.25],
                 index=[2, 4, 8, 6])
ser1+ser2
```

We have two Series objects, `ser1` and `ser2`. 

The two have both matching and unmatching indices. 

We've then tried to align the values of the two Series objects based on their labels.

The code should run as follows:

![](Capture11.png)

Where no matching labels were found, the result is `NaN`.

### Indexing NumPy Arrays is faster than Indexing Pandas Series Objects

The reason is that Pandas does a lot of work when you index. 

It has to align the Series on their indexes before doing operations. 

If the Series objects are already aligned, that will be wasted processing. 

## Conclusion

This is what you've learnt in this article:

- A numpy array is a grid of values that belong to the same data type. 

- NumPy arrays are created using the `array()` function. 

- A Pandas Series is a one-dimensional labeled array that can store data of any type.

- It is created using the `Series()` function of the Pandas library. 

- Both array and Series values can be accessed using their corresponding indices and the square bracket notation. 

- The Pandas Series has an explicit index defintion, which gives it additional capabilities compared to the numpy array. 

- The indices of a Pandas Series must not be of an integer data type, but they can take other data types like strings. They can also be non-sequential or non-contiguous. 

- Operations between Series objects automatically align data based on the label during alignment. 

- If no matching labels are found, Pandas returns NaN.

- Pandas does a lot of work during indexing, hence, it is faster to index numpy arrays than Pandas Series objects. 

















