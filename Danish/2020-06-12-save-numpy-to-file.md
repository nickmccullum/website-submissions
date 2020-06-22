---
title: 'How to Save a NumPy Array to a File'
date: 2020-06-22
author: Danish Yasin
layout: post
permalink: /save-numpy-to-file/
---


# How to Save a NumPy Array to a File

The beauty of Python is in its ability to work with a diverse range of datasets in a very optimized manner. If you’re even a beginner in Python, then you must have used the four non-primitive data structure of Python, which are: 



1. Lists
2. Tuples
3. Dictionary
4. Sets

These data structures are very useful when dealing with common problems and can handle all sorts of data types. 

However, if you’re working in the domain of Machine Learning (ML) and building ML models then you regularly require the use of a highly optimized data structure like NumPy arrays. ML models present in libraries like scikit and Keras usually expect input and produce output like predictions, in the form of NumPy arrays. 

Keeping these things in mind, knowing how to save NumPy arrays to a file is a common requirement for all data scientists.

You can use the NumPy arrays to store predictions outputted from a ML model or create an array to store any other important information that you need to access quickly and efficiently. 

When dealing with especially numeric data, using NumPy arrays over other data structures makes sense as NumPy provides a number of inbuilt methods that can help you work on your data.

In this tutorial, you will be learning about how to save the data stored in a NumPy array onto different kinds of files. The tutorial will cover three use cases: 



*   Saving NumPy array to a CSV file
*   Saving NumPy array to a NPY file
*   Saving NumPy array to a compressed NPZ file

Let’s start and take a look at how you can save data stored in a NumPy array onto a CSV file. 


## Saving NumPy Array to a CSV File 

Comma Separated Value files are the most commonly used file format for storing numerical data. It makes sense that you would be using a CSV file to store your NumPy array. The data could be the parameters that a ML model outputs or some other form of data.

You can easily save your data by using the `savetxt()` method of NumPy. In the parameters, you insert the name of the CSV file, the variable that stores the data and define the delimiter used in your data. 

The delimiter is the character that separates each value in the data. This will be used for placing data in separate columns in the CSV file and can be set by defining the `delimiter` in the parameters of the method. 

Let’s take a look at an example of how you can store a NumPy array onto a CSV file: 

```python

# Importing the NumPy package

from numpy import *

# define data

NumpyData = asarray([[20, 48, 39, 100, 71, 45, 1, 21, 15, 9]])

# save to csv file

savetxt('NumpyData.csv', NumpyData, delimiter=',')

```

In the above code block, you are simply importing the numpy package and then defining the `NumpyData` as a numpy array by using the `asarray()` method. 

Afterwards, you are simply saving the initialized array `NumpyData` to a csv file by using the `savetxt()` method that takes the name of the csv file, the variable containing the numpy array and the delimiter as parameters. 

On running this short script, you will get a csv file as output, which is named `NumpyData.csv` here. On opening the csv file, you’ll be able to look at all the data stored in your numpy array. 


<table>
  <tr>
   <td>2.00E+01
   </td>
   <td>4.80E+01
   </td>
   <td>3.90E+01
   </td>
   <td>1.00E+02
   </td>
   <td>7.10E+01
   </td>
   <td>4.50E+01
   </td>
   <td>1.00E+00
   </td>
   <td>2.10E+01
   </td>
   <td>1.50E+01
   </td>
   <td>9.00E+00
   </td>
  </tr>
</table>


You’ll notice that the data has been correctly saved in a single row as intended and the precision of the data is visible as well. 


### Loading Data from CSV to a NumPy Array

You can not only save data to a csv file but also read from it by using the `loadtxt()` method. Let’s see how you can read the data from the csv file you created above and store the data in a numpy array. 

```python

# Importing the NumPy package

from numpy import *

# Load Array

NumpyData = loadtxt('NumpyData.csv', delimiter=',')

# Print the array

print(NumpyData)

```

Running the code will yield the following output:

```python 

[ 20.  48.  39. 100.  71.  45.   1.  21.  15.   9.]

```


## Saving NumPy Array to a .NPY File

Saving the data onto a csv file is great if you are trying to distribute the data or use it for research later on. However, if you want to efficiently store data present in a NumPy array and use it only for other Python programs then you can store it in .npy files. 

Saving the numpy data into .npy files increases the efficiency of saving and loading data as it is stored in a native binary format. 

Using .npy files is common for when a particular data set needs to be cleaned, transformed and prepared to be used in the testing of a machine learning model in the future. 

The .npy format is also known as the “Numpy Format” and data can be easily stored in a .npy file by using the inbuilt method of `save()` of the NumPy package. 

Let’s take a look at how you can store your numpy array to a .npy file: 

```python

# Importing the NumPy package

from numpy import *

# define data

NumpyData = asarray([[20, 48, 39, 100, 71, 45, 1, 21, 15, 9]])

# save to csv file

save('NumpyData.npy', NumpyData)

```

In the above code block, everything is the same as in the previous section except for the last line where the data is being saved by calling the `save()` method. 

After you run this script, you’ll find a new file by the name of “NumpyData.npy” in the same directory as the script. 


### Loading Data from .NPY file to a Numpy Array

Let’s try to read data from the numpy file we created earlier. This should be fairly simple and quick. Take a look at the following code block: 

```python 

# Importing the NumPy package

from numpy import *

# Load Array

NumpyData = load('NumpyData.npy')

# Print the array

print(NumpyData)

```

If you run the above explained script, you will get the data from the numpy file and it will be printed on the console, like: 

```python

[[ 20  48  39 100  71  45   1  21  15   9]]

```

Now let’s take a look at what to do if you have a really large data set and it needs to be reused in multiple projects. 


## Saving NumPy Array to a .NPZ File 

The answer to what you should do if you have a large data set that needs to be reused in multiple projects is that you should use the .npz file format. 

The data could be a collection of images in pixel format or collection of some other data, you would want to store it in compressed format to save storage. 

By using .npz files, you can compress a dataset in the size of gigabytes to the size of megabytes. This will allow you to easily transfer your data from one place to another and is especially useful if you are transferring data onto the cloud as it will help save bandwidth. 

The .npz file format is basically a compressed version of the numpy file. 

Let’s take a look at how you can store a simple numpy array to a .npz file: 

```python

# Importing the NumPy package

from numpy import *

# define data

NumpyData = asarray([[20, 48, 39, 100, 71, 45, 1, 21, 15, 9]])

# save to csv file

savez_compressed('NumpyData.npz', NumpyData)

```

If you run this script, you will find another file with .npz extension in the directory, the name of which will be “NumpyData”, if you run the script as is. 

With the .npy and .npz file formats, you cannot view and inspect the content of the files because the data is stored in the binary format. 


### Loading Data from .NPZ file to a Numpy Array

As mentioned earlier, .npz file is basically a numpy file but compressed. The file format supports the storage of multiple arrays into a single file. 

You can read from the .npz file the same way you read data from the .npy file with one difference. Since a .npz file supports storage of multiple arrays, therefore, you get the data from the .npz file in the form of a dictionary. 

The keys of this dictionary are named as ‘arr_n’, where n is the number of arrays, starting from 0. 

Since in our case, there is only one array present in the “NumpyData.npz” file, the array will be present in ‘arr_0’. 

Let’s try to access the data: 

```python

# Importing the NumPy package

from numpy import *

# Load Array

dictData = load('NumpyData.npz')

NumpyData = dictData['arr_0']

# Print the array

print(NumpyData)

```

If you run this script, you’ll get the output: 

```python

[[ 20  48  39 100  71  45   1  21  15   9]]

```

Hence, in this way, you can access the data from a .npz file and store it in a numpy array. 


## Conclusion

Learning how to work with numpy arrays is an important skill that you would need to learn to progress in your data scientist career. This tutorial was limited to just explaining how to store and access data from numpy arrays to different file formats. 

There is a whole lot more to numpy arrays that you should study and learn to use as the methods provided by numpy are very useful when it comes to scientific calculations. 