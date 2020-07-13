# Python Pandas: loc vs. iloc for Accessing Data

Python is among one of the very few languages that are suitable for data science. The ecosystem of Python is very rich and sophisticated in terms of making it easier for data scientists and engineers to manipulate data and extract resourceful information out of various datasets. Pandas is one of these libraries that make this Python ecosystem further facilitating by introducing higher levels of flexibility into the workflow of data scientists.

In this tutorial, we will get ourselves familiar with two of the widely used functions to select and filter data from Pandas dataframes.

In case you do not have Pandas, go ahead and complete the installation with,

`pip install pandas`

  

We will also need a dataset in order to get ourselves familiar with the functions we will be going over today. In this tutorial, we are using the [World Happiness Report 2015 dataset from Kaggle](https://www.kaggle.com/mathurinache/world-happiness-report/data). However, feel free to use your own dataset.

Let’s download a dataset of your choice and import to our script.
```python
import pandas as pd
df = pd.read_csv('dataset.csv')
```
  

If we look at the shape of the dataset, we can see that it has 158 rows and 12 columns.

`df.shape`

  

Output:

    

> (158, 12)

  

Let’s take a look at the first 5 rows of the dataset.

`df.head()`

  

Output:

![](https://lh4.googleusercontent.com/98rUou_-iG_YytnUEDDeh_vpmOCXaRysZCNDUwmKbtSEdPpUYjMgBGcynZRtYTcXgVKVpD7PChn86etflVxQG24k_QY3WWMLXFCBVCo6KaD8_YfLMNx60Z8CvPObEx9hZGvItNc)

Now we are ready to get started. We will first look at the rudimentary way of selecting and filtering data from the dataset.

## Selecting Data from Dataframes: A Rudimentary Approach
    

### Selecting Columns by Column Name(s)
    

Let’s retrieve the first five rows of the columns ‘Country’ and ‘Happiness Score’.

`df[['Country','Happiness Score']].head()`

  

Output:

![](https://lh4.googleusercontent.com/rittnJt1BTYLweKELs6qwPvftrKyZ7qUqbqwY5fCRbRgboONunRYUap8ttilfF9QMUTuLlLF5olnAzj7HrAyrwMb8j7CqbdETSYFdleRaATrzP_dfCIy2SjqhMAPeyFsBd4pEBc)

  

In this, we are sending a list of the columns we want to retrieve. We can add more columns to the output dataframe by appending the required column names to the list.

### Selecting Columns by Data Type(s)
    

We will now look at how we can retrieve columns by their datatype. In this, we are passing a list of the datatypes of the columns we require as the include parameter to the `select_dtypes()` function. Let’s retrieve all string values from the columns.

`df.select_dtypes(include = ['object']).head()`

  

Output:

![](https://lh5.googleusercontent.com/i4REe6E-MoPEWYKMCH3KrfY8rJUhnb8fP07hgdZAY1hZlgVqltVbtLP0-NbPps9PxPUpIgjSWdYpxtZKEnUPNKt5NY03okajcXZu4pmt2sm_UnXIcviwPwp9bZElygMoWDEFDHw)

Instead of ‘str’, we are using the datatype ‘object’ here. We will now retrieve both string and float values.

`df.select_dtypes(include = ['object', 'float']).head()`

  

Output:

![](https://lh3.googleusercontent.com/Yfv5zwujiOmRUsO8sQGE3uAm7cf1yIe1Q5ocK8vKmWt8gdnW5RWBjcO2bWmC9VwOe-mfdJNYXJBG--Yb3eOOr_mWZSsuaal-scVzLL7bq_9X2fgBhat8Lwhgp6IuGzck1HaxB6U)

Since the whole dataset only consists of the above two data types, it will output all the columns.

### Selecting Columns by Filtering
    

We can also use the `filter()` function to retrieve data from columns that have a substring of our choice in its column name.

`df.filter(like='Score').head()`

  

Output:

![](https://lh5.googleusercontent.com/-DTpnxYVGLCne3nM2s1VRmsk4i7a4l1cOZoeKbD7Aob6Cvwjtt6TPpYSD5tn7kp3CocB0YAELFl3JzoxtJ03nHjGlJroiyI8isPDdURDIxrLnI98LItP-Syj7fIV-nGKGrJX53E)

We will also receive multiple columns if the substring of choice is being contained in any of the other column names.

Now that we have a fair idea about how to retrieve data from a dataframe, we will next look at two of the most versatile functions built into Pandas: iloc and loc.

## Selecting Data from Dataframes: iloc
    

iloc in Pandas is used to make selections based on integer (denoted by i in iloc) positions/ indices. That means we can retrieve data by using the position rows and columns are present in the dataframe. We can visualize that the rows and columns of a dataframe are numbered from 0. We can use this logic to retrieve data using iloc.

Let us go through an example first.

We will pick the first row of the dataset.

`df.iloc[[0]]`

  

Output:

![](https://lh6.googleusercontent.com/dxHlBzqg2UkNbG2GcN03JtoVAArXOkFfXPjfRdn_k4cTVNPzQ7Wv6QuUUo3fbNXW_Zs12KHMsDuK3EBArkVtK4blOolqH1yOUEU3Csd-dRr5CzJ42eh19XK_AUEM6-JW9HzrvyQ)

We can also pick multiple rows using the same method.

`df.iloc[[0,25,30]]`

  

Output:

![](https://lh5.googleusercontent.com/wbHCLMFmhfM25FnWWcjx-tuKTf-mwCzk6oplIC8SM7yfaU7A2ZHP6f89y7grs7uKROX5AJ4jhTY2d15jJrkX9W-BBnvczyji8M3pxGPtfI5SrDCM55mwb7Pa4i7UwXFDHAQfIp4)

We can also pick the last row without knowing how many rows there really are. We can pass a list with the element -1 as follows.

`df.iloc[[-1]]`

  

Output:

![](https://lh3.googleusercontent.com/hzgfH2jB4YznZAOgOiKEnMtBf0AdWrAGMQgIaXAN2-lHiYBuR__R-j8M-AknLViZMK37xajW59r3DN6LLiQEa0iL9Tm5Hb_Ws7lV7kLau6VmxKjNmq82CXuSaOQLo6UqUCIvETc)

  

We will now pick a column the same way. If we look at the structure of iloc, it is such that we specify the intended rows we plan to receive in the first list and the intended columns in the second list. Although this might look tricky and complex, it really is as simple as retrieving a row.

`df.iloc[ :, [0] ].head()`

  

Output:

![](https://lh5.googleusercontent.com/BiiZqo7bj-fZMotTSKxZJfSsxzAK7Jtlb0UXtEfulFgn-DTAfEuHfZMzsHQa6HjCNiDS69YCBOXW6BcAKJXatajPtTEH2emOM_yFz2zghRCcDAPbfISkmpkn7HzZkhkDZ4Yt8ag)

  

We can also retrieve the last column by passing -1 to the list as we did before.

`df.iloc[ :, [-1] ].head()`

  

Output:

![](https://lh4.googleusercontent.com/ckP5pJrImEIjDBBOyV8xCCA2ogcNOkk0raO3Tqdgf6m-jqiG5jsbaY_Rag4TKSy-8waH7YZUDV5DhjEmf1_uzZ45RP3Q2riXAQGzefVgfLo2V_jTVvEnyMXqBFfdOToVrOtzRBk)

We can combine both the row and columns lists we learned to retrieve data elements from various positions of the dataset. Let’s say we want to retrieve the first cell, which happens to be the data element in the first column and the first row.

We will be retrieving it as,

`df.iloc[ [0], [0] ]`

  

Output:

![](https://lh5.googleusercontent.com/GyAx7bITiBNFWlq5C6ruxEWo_Bh-2R9Xh_Lg04hSOwdJeIf7UDRoXTUmY-ag388ONfwDmwXYEN3pwmxwY2rQ4jXtEMkHANggsfQXtmcJH0aDDp6DmfaViJxleGq3La2_pxxMes4)

  

We can play around with this trying to retrieve various data elements. Let’s retrieve the Happiness Rank and Happiness Score for the 0th, 25th, and the last observations of the dataset. We can identify that the Happiness Rank and the Happiness columns are the 2nd and the 3rd columns of our dataframe. Therefore, we can retrieve these data as follows.

`df.iloc[[ 0 , 25 , -1 ],[ 2 , 3 ]]`

  

Output:

![](https://lh3.googleusercontent.com/2SXbijYAlsEvPdN-yYsG3kf8e6qWyWvxYSZcixW8MAMglWAvyjcmR_JS6Ww8mIvquBV5nY9BXjAsyRaN6EqnufZwVWtHTylho6Rc4teiJ8cCqEYeRhlbnuS3ci6oJ1nFAtGRrco)

  

If we are to select rows and columns between a range, we can treat the indexer the same way we treat arrays.

Let’s select Happiness Rank and Happiness Score data from the rows 30 to 34.

`df.iloc[ 30:35, [ 2 , 3 ]]`

  

Output:

![](https://lh4.googleusercontent.com/lLHDTqUpo4d07vGe3eTszbYmaKOx-reHn9n8FboW_20jZfNr4U_zJYdlYNRCvMC9c24yWrCz7-64AB7zRvxka6b6ZEeYoSCMSpCdQH8v4tUx1m0ffXAiiZjPNaf2w1d_Rrmgro0)

  

One of the important things to keep in mind is that when we specify the range, it always runs from the starting number to the number right before the interval ending number. For instance, if we say [0, 5], it means that we are considering a range that runs from 0 to 4.

Now that we have familiarized ourselves with iloc, let us look at the next indexer in line: loc.

  

## Selecting Data from Dataframes: loc
    

loc in Pandas can be used in main two approaches when we are working with data. We can use loc to retrieve data elements based on their indices or labels and we can use loc to retrieve data using conditional statements. We will now look at each of these separately.

### Index-Based Data Retrieval
    

If we recall what we learned in the last section, we understand that we used iloc to retrieve data based on their position or the location in the dataframe we were considering. For instance, if we execute df.iloc[[0]], it will output the first row from the dataframe. Even if the index of that row was a different number than 0, it would have returned the first row from the dataframe as we would perceive it.

However, when it comes to loc indexer, it works a little differently than the iloc. It will always call the data elements by their specified index. Let’s consider an example.

`df.loc[[0]]`

  

If we run the above, it will output the following.

![](https://lh4.googleusercontent.com/X2sKxoVcbAp5qKd-SNaEqnoCGsaKChJ_mRpMYV32OcfLpGDhnUQu6A7eWGi1BBSqCl3a1OUtA-gFhcgkoHzZErksQs3S6UZuvrD_ShtfAu0Mi62oGIhy-Wo-uPJTkiUy8BLcS2E)

The result was the same result that was produced by iloc earlier in the previous section. Let us now change the index of the dataframe to a different field. Let us set it to Happiness Rank.
```python
df.set_index('Happiness Rank', inplace=True)
df
```
  

Output:

![](https://lh4.googleusercontent.com/2m64Fnq9KSNc6o4-K8ouoblc_LL7PGKRV8j6cOcf220H98Pqc3zFD5EY9CoDbPAQmls_WG-h1enVfSN3U1KY7kf3ra7XUpdk9fZT0k3G8TYbd3LN9pHalbAhxxPg63XLKrojCw8)

We can see that the index has been changed to Happiness Rank and now it starts from 1 opposed to the original dataframe that started with 0.

Let us now run iloc and loc again.

-   iloc
    

`df.iloc[[0]]`

  

This will output,

![](https://lh4.googleusercontent.com/F2zVobIQQ0VHr6fYcn4fJstM7qTOmSeLRqhu4m9JtQMg4-xLxoueCxh71iCcXmPqh2e98U4IUU5IDAbahTv_WUPvv3RUCCqJWVkUH8VaLws9ZeFITYBlHN4JjAr5eCKksSjmfOM)

As we can see, the result is the same as before except for the index, which is 1 now.

Let us run the same for loc.

-   loc
    

`df.loc[[0]]`

  

Output:

> KeyError: "None of [Int64Index([0], dtype='int64', name='Happiness
> Rank')] are in the [index]"

As we can see, running the same with the loc indexer gives us a KeyError. If we go back to the current df version, we will see that this happens as there is no index with 0 in the updated dataframe since we changed the index field to Happiness Rank which starts from 1 instead of 0 as before. We can run the following with the updated index instead to retrieve the same element as before.

`df.loc[[1]]`

  

Output:

![](https://lh4.googleusercontent.com/F2zVobIQQ0VHr6fYcn4fJstM7qTOmSeLRqhu4m9JtQMg4-xLxoueCxh71iCcXmPqh2e98U4IUU5IDAbahTv_WUPvv3RUCCqJWVkUH8VaLws9ZeFITYBlHN4JjAr5eCKksSjmfOM)

  

Let us change the index to the Country field now. However, we have to make sure that we reset the index and have the Happiness Rank as a field again as before.
```python
df.reset_index(level=0, inplace=True)
df
```
  

Now we can see that the Happiness Rank is back as a field.

![](https://lh3.googleusercontent.com/bLzAMWIWZBJHRA4hEdA8Skmbsb8ILFra3LZelGROS5RW2XwmWvSOnaqoQtZx6LuLJ3MfS1cg0VWVxsFigIKMOR82rZmGDld2K4M_VFfnPdUAAwT_fr31llz6l5XFvjxPVp0eTCU)

We can change the place of the column to be the same as before. However, we will not spend time on that as it is not a necessity here when we are using loc. Let’s set the index to the Country field now.
```python
df.set_index('Country', inplace=True)
df
```
  

Output:

![](https://lh4.googleusercontent.com/tbkDVMZ2E3jwCviJj_1arisBs7P7MAn_dZ4KcH3TI4hqhBVg1K-ZpmrH7MstV780GjYvMtEGRa8l_iOx_aYfWY1N8RBrR2EW0v_ZsEYiQs2dcCUxgXovWT8Tqq98pdjGGiXipFY)

  

Let us run iloc to retrieve the first row.

`df.iloc[[0]]`

  

Output:

![](https://lh3.googleusercontent.com/_NJbhad9hCa5qry3bDKZcI1Nyfpg8Qdi9HPS3sW-V_zdZwAkshbm0OV6RoQK45Zdxh6c9gCr2lF2ajRmhHAsrFmh2XaE5B1L67KxM5i-9sswDebOoZYxoG9kZ3GyujiJ0u6KF1A)

If we are to retrieve the same data using loc, we will have to use the index value. In this case, it will be ‘Switzerland’.

`df.loc[['Switzerland']]`

  

Output:

![](https://lh3.googleusercontent.com/_NJbhad9hCa5qry3bDKZcI1Nyfpg8Qdi9HPS3sW-V_zdZwAkshbm0OV6RoQK45Zdxh6c9gCr2lF2ajRmhHAsrFmh2XaE5B1L67KxM5i-9sswDebOoZYxoG9kZ3GyujiJ0u6KF1A)

With that, now we know how differently iloc and loc behaves when they are retrieving elements.

We will now look at a few use cases performed on the updated dataframe with the index as the Country.

Let’s retrieve data for two countries, Denmark and Panama.

`df.loc[['Denmark','Panama']]`

  

Output:

![](https://lh6.googleusercontent.com/X4Xr541Goc36cP6HIoj5NAj1VrzlD7AM2EIqaPX7v_ec7y9VCkiM6DaJVNNIjFhePeYxktwt9dQhsk6VYW45RSWBpQgg0GApvXRcwfLStaPKd8wkrwlMtP3gGAmIq6ebLLV6lgs)

If we are writing functions for our custom programs to retrieve data based on the index, instead of querying explicitly, we can set the index as the field we want and retrieve the information using loc this way.

Let’s retrieve the Region and Happiness Score of Australia and Sweden.

`df.loc[ ['Australia','Sweden'], ['Region', 'Happiness Score'] ]`

  

Output:

![](https://lh3.googleusercontent.com/4_mkFH8wQsjVop3FdZpCAGtOO4DKWIpn-ZXLK964sD-6MzeJzhgV8BasB6hxbiTgYthZr31e24ashMyUcpJaGgW6kyJOa4calfU8JVeXcV5Kjcltc62O6UV8GyJ1hYA3QheqJTw)

Instead of typing the column names, we can also pass the column index from df.columns. Before we do that, let’s get ourselves familiar with the df.columns property.

`df.columns`

  

Output:

> Index(['Happiness Rank', 'Region', 'Happiness Score', 'Standard Error',
>            'Economy (GDP per Capita)', 'Family', 'Health (Life Expectancy)',
	> 		'Freedom', 'Trust (Government Corruption)', 'Generosity',
	> 		'Dystopia Residual'],
	> 		dtype='object')

  

We can access the column names using the index as follows.

`df.columns[0]`

  

Output:

> 'Happiness Rank'

  

Let’s now retrieve the Region and Happiness score as earlier from the same two countries, Australia and Sweden.

`df.loc[ ['Australia','Sweden'], [df.columns[1],df.columns[2]] ]`

  

Output:

![](https://lh3.googleusercontent.com/4_mkFH8wQsjVop3FdZpCAGtOO4DKWIpn-ZXLK964sD-6MzeJzhgV8BasB6hxbiTgYthZr31e24ashMyUcpJaGgW6kyJOa4calfU8JVeXcV5Kjcltc62O6UV8GyJ1hYA3QheqJTw)

  

We will now look at how to retrieve data based on different conditions.

  

### Condition-Based Data Retrieval
    

The usual and logical approach for us to retrieve a certain data element depending on the content of it could be a problem that can be solved using for loops and if conditions. Let’s say we are trying to find the rows with Health (Life Expectancy) above 0.95. Instead of using for loops, we can find these in a much more optimized way using the loc indexer.

`df.loc[ df['Health (Life Expectancy)']>0.95 ]`

  

Output:

![](https://lh4.googleusercontent.com/ZXRWu7a-jAgbmFvfSyb0k03ukXxP3vcPESBR82IQW0xQ_M51Aa0mwJmwZSFnPTafYQHsWzmA-zIxeYHcMy0lDPMxZyncQ_fxuc_LFuw4ggOVjTYyBbnv8L_aa7BWzlYIucWy5R4)

  

Let’s say we only want the Happiness Rank and the Generosity of these countries. We can easily include the required column parameters as follows.

`df.loc[ df['Health (Life Expectancy)']>0.95 , ['Happiness Rank', 'Generosity'] ]`

  

Output:

![](https://lh6.googleusercontent.com/nAc62jDURNWNdDX0Oxk7ln-htDw4-XIUc8v64ccLPNTqFVzI_2uwhG3uCVXSMXTzHid9VSK4oYORpBkkVOACrNCzOhEnxlSngH101M9prfTohimp1WWSTmQzpUG9L0Jw4yltzxE)

  

We can also have multiple conditions specifying what data we are looking for. Let us retrieve countries above 0.95 Happiness Scores and also are from the Eastern Asian region.

`df.loc[ (df['Health (Life Expectancy)'] > 0.95) & (df['Region'] == 'Eastern Asia') ]`

  

Output:

![](https://lh5.googleusercontent.com/jA14TbMRDV9TctXbo4RhqPsmKoM4_D5YKrUrbj_1pA2ZWeEJ_r2T5E6vdVuWykWU5-214XKAs7q_EixAiR5cp2TKOTZG34iJTK6b2PXPSD5CA50zWyv25dds2y2Bz9uOeKfrOsg)

  

Now that we have covered the basics and got ourselves familiar with the functionality of loc and iloc indexers, we will now take a look at their data types. Most Python developers tend to think that whenever we receive a table as an output, it necessarily has to be a dataframe. However, this is not the actual case. In reality, when we are retrieving data, although they may look alike, their underneath type can be different. We will now take a look at a few of the types of Pandas objects iloc and loc indexers produce.

Let’s consider the following.

`df.iloc[0]`

  

Notice that we have used the value straightaway instead of passing a list with the value.

Output:
![](ouput1.PNG)

  

In this, we realize that instead of printing the dataframe as a horizontal table, we can also access it as a series and have a link to individual values based on indices.

Let us confirm this by executing,

`type(df.iloc[0])`

  

Output:

> pandas.core.series.Series

  

Let us observe what happens if we do the same by passing a list with the index.

`type(df.iloc[[0]])`

  

Output:

> pandas.core.frame.DataFrame

  

Although these may seem trivial, it is at the real-world implementations of these functions and their basics we learn that will be useful.

## Conclusion
    

Pandas library is one of the most favourite Python libraries of all time. As we play with lots of data in Pandas, it is always resourceful to be familiar with in-built functions that are much more optimized and easier to use than writing entire codes to execute a certain data manipulation or filtering task. iloc and loc are two of the very popular and highly important indexers. In simple terms, iloc is used in circumstances where the data are being retrieved based on their position in the dataframe. loc is used to retrieve data based on their indices rather than the position.
