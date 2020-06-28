# How to Clean Text for Machine Learning in Python

  

Textual data plays a huge role in machine learning. They are also one of the key types of data in addition to numerical data values. Texts are used for various applications in machine learning such as language translation, sentiment analysis, content detection, and even developing chatbots. All these require massive amounts of textual data in order to produce successful results. As much as textual data is rich in useful content, most of them are highly disorganized, unstructured, and often contain noise. This is why we are required to clean texts before utilizing them to train our machine learning models.

Let us first get an idea about the important components of a text we need to consider when we are getting started with the cleaning process.

## What Should We Notice in Textual Data?
    

Textual data can take many forms. For this example, we will be using [Pride and Prejudice](https://www.gutenberg.org/files/1342/1342-0.txt) by Jane Austin that is available under Plain Text UTF-8 as a .txt file on [Project Gutenberg](https://www.gutenberg.org/). However, feel free to pick any other book or document to get familiar with the components and aspects of any common document we need to keep an eye out for.

Depending on the document we pick, we will notice different components and patterns of the text. As we go through the Pride and Prejudice plain text file, we will first see the licensing and copyright information. It is then followed by the content and then the story starts. We can scroll through the story and notice the following.

-   Each chapter starts with a designation ‘Chapter’ followed by a number.
    
-   There are normal sentences as well as dialogues.
    
-   We can identify dialogues with the double-quotes wrapped around them. We can identify a conversation between people with alternating double-quote encapsulated sentences and paragraphs.
    
-   There are underscores (_) wrapping some words.
    

  

These were a few aspects that could be noticed in the text we picked. Depending on the text you have picked, we will come across different patterns and textual components. As cleaning text is a very specialized task that will differ from one another depending on the machine learning model, it is up to the developer to decide on how the cleaning process should be. However, there are always a few general tasks that can be added to the cleaning process. We will take a look at them in the next section.

  

## Basic Data Preprocessing
    

Data preprocessing is an essential component of any text cleaning task. This step will consist of many micro-steps that will be highly useful for the whole process. In this section, we will be looking at the most basic preprocessing steps that require no additional or third-party libraries in Python to implement. In order for us to understand what we are doing, we will go over these preprocessing tasks one by one and try to perform each task from scratch.

  

### Tokenization
    

Tokenizing is the process of splitting sentences, paragraphs, or even the whole document into words or phrasal units. Each unit is called a token.

Before we tokenize a whole text, let's understand what happens.

We will write a sentence below.

  
```python
my_text = 'Wisdom is acquired when hiding with a saucepan on your head.'
```
  
  

We can start tokenizing our sentences by using Python’s `split()` function which returns a list of strings consisting of the words from the sentence.

  

`my_text.split()`
  
  

Output:

  

> ['Wisdom', 'is', 'acquired', 'when', 'hiding', 'with', 'a',
> 'saucepan', 'on', 'your', 'head.']

  
  

Split() function separates strings using the space character by default. However, we can specify the separator by sending the character or the string as a parameter into the split() function.

We will use 'when' as our separator and see what happens.

  

`my_text.split('when')`

  
  

Output:

  

> ['Wisdom is acquired ', ' hiding with a saucepan on your head.']

  

We can also use regular expressions in tokenization. Regexes simply are sequences of special characters that can be used to match with existing strings as a pattern.

In Python, we can use the re module for this.

Let’s import the re module first.

  
```python
import re
```
  
  

We will now use ‘[\w']+’ as our special character sequence. ‘[\w']+’ basically means we are looking for sequences of characters with alphanumeric characters separated by other characters that do not belong in the specified sequence by the regex.

  
```python
re.findall("[\w']+", my_text)
```
  
  

Output:

>     ['Wisdom', 'is', 'acquired', 'when', 'hiding', 'with', 'a', 'saucepan', 'on', 'your', 'head']`

  
  
  

### Removing Punctuation
    

It can be seen from the last regex example that the full stop punctuation character has been removed from the list of tokenized text. In the same way, we can configure a sequence to remove punctuation from a string as we please. However, in this case, there is a better and more efficient way to get the same task done by using the character mapping function and dropping the punctuation characters.

We can easily get all the punctuation characters from the string module.

  
```python
import string
string.punctuation
```
  
  

Output:

> '!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~'

  

We can use the translate() function with parameters as a mapping table created using the maketrans() function. In maketrans() function, we can pass parameters as mapping characters and the dropping characters. We can do it below.

  
```python
import string
my_text = "How's it going?"
my_text.translate(str.maketrans('', '', string.punctuation))
```
  
  

Output:

> 'Hows it going'

  
  

Then we can tokenize our new output.

However, imagine that we are to remove punctuation from the list of tokenized texts.

  
```python
my_text = "How's it going?"
my_text.split()
```
  
  

Output:

> ["How's", 'it', 'going?']

  
  

We can easily perform this by iterating through the list as follows.
```python
import string
my_text = "How's it going?"
my_tokens = my_text.split()
[token.translate(str.maketrans('', '', string.punctuation)) for token in my_tokens]
```
  
  

Output:

> ['Hows', 'it', 'going']

  
  
  
  

### Case Normalizing
    

When processing texts, it is a usual practice to keep all texts in the lower case as to avoid any potential confusion. However, it should be kept in mind that this might not be very constructive in some cases where names and words like Amazon and amazon are existing in the vocabulary of the potential machine learning model.

Let us now see how we can easily normalize the case using Python.

We can normalize the text before it is tokenized as follows.
```python
my_text = "I am doing good."
my_text.lower()
```
  

Output:

> i am doing good

  
  

However, it can also be performed after the text tokenization is performed.
```python
my_text = "I am doing good."
my_tokens = my_text.split()
[token.lower() for token in my_tokens]
```
  
  

Output:

> ['i', 'am', 'doing', 'good.']

  
  

## Advanced Data Preprocessing
    

Now that we know the basic steps in the preprocessing, we will look at more preparations that we can take while cleaning our texts. In this section, we will be using the Python Natural Language Toolkit (NLTK) to implement the respective steps.

Let us first install NLTK.

`pip install nltk`

  
  

Now let us the required data for the module to perform.

Run the following in your terminal or the command prompt.

`python -m nltk.downloader all`

  
  

Now we are good to go Let us now go over the following one by one.

  

### Removing Stop Words
    

Stop words are known as words with no significant semantic value. For example, 'the’, ‘is’ are stop words. However, in the event the potential model being a natural language processing system or a chatbot, this process might be counter-intuitive.

Let us find what are the stop words NLTK identifies in its corpus module.
```python
from nltk.corpus import stopwords
stopwords.words('english')
```
  

Output to this is a list of stop words. If we print the first five words, it will output,

> ['i', 'me', 'my', 'myself', 'we', 'our']

  
  

In the NLTK version this tutorial was done, the list goes on up to 179 stop words.

  

Let us try to remove the stop words in the sentence 'I am doing good'.

  
```python
from nltk.corpus import stopwords
my_text = "I am doing good."
my_tokens = my_text.split()
stop_words = set(stopwords.words('english'))
[token for token in my_tokens if  not token in stop_words]
```
  
  

Output:

> ['I', 'good.']

  

From the output, it can be understood that both ‘am’ and 'doing' are stop words in the NLTK corpus. The idea here is that the potential machine learning model only requires the above two words to make sense out of the whole sentence.

  
  

### Stemming
    

Stemming refers to the process that drops unnecessary characters from tokens or words. Stemming really becomes helpful in classification tasks when the size of the vocabulary is required to be kept at a minimum level and make a surface-level sense of all the inputs.

There are many stemming algorithms in existence and in this, we will be using the popular Porter Stemming algorithm to drop the morphological and inflexional endings of the tokens.

Stemming of the word ‘playing’ would result in ‘play’. The stemmed version of ‘player’ would also be ‘play’. However, if we stem the word ‘studies’, the output would be 'studi' which will not make much sense to a human reader. Surprisingly, stemming the word 'studying' would result in 'studi' as well.

  
```python
from nltk.stem.porter import PorterStemmer
my_text = 'I am studying the studies of academia'
my_tokens = my_text.split()
porter = PorterStemmer()
stemmed_tokens = []
for token in my_tokens:
	stemmed_tokens.append(porter.stem(token))
print(stemmed_tokens)
```
  
  

Output:

> ['I', 'am', 'studi', 'the', 'studi', 'of', 'academia']

  
  

### Lemmatization
    

Lemmatization is somewhat similar to stemming as well. It is also used to drop inflexional endings of different word forms. However, the end results are much different from stemming. Consider the following.
```python
from nltk.stem import WordNetLemmatizer
lemmatizer = WordNetLemmatizer()
print('studies :', lemmatizer.lemmatize('studies'))
print('studying :', lemmatizer.lemmatize('studying'))
```
  

Output:

> studies : study 
> studying : playing

  
  

If we were to lemmatize nouns, it would result in its singular form as follows.
```python
from nltk.stem import WordNetLemmatizer
lemmatizer = WordNetLemmatizer()
print('genii :', lemmatizer.lemmatize('genii'))
print('radii :', lemmatizer.lemmatize('radii'))
```
  

Output:

> genii : genius
> radii : radius

  

This stage pretty much concludes the text cleaning process. The next stages include text embedding followed by feature extraction. However, both those stages are often considered to be post-cleaning steps. Either way, we will get to know a bit about both of them as it is much closer to the data processing stage.

### Text Embedding
    

Embedding denotes transforming the tokens into a number in order to prepare them to be represented as mathematical vectors on the vocabulary hyperspace. These vectors are expected to be running towards approximately similar directions if their semantic meanings are similar. For instance, ‘love’, and 'affection' is expected to have the same directions while 'good' and ‘bad’ have totally different directions.

  

Once the text is cleaned and tokens are embedded, next is the feature extraction stage. The idea is to give the embedded tokens with the numerical representation a semantic notion using different tools. The more recent researches and applications use techniques like Bag-of-Words, Word2Vec, and Glove.

  

Depending on the nature of your task, there are a few additional things to look out for after data has been pre-processed before the embedding stage.

  

## What Other Aspects of Texts Should We Look for?
    

Text cleaning is a highly dependent process and can differ from one machine learning model to another. However, across various models and various text files, there are some facts which require to be considered at least slightly.

-   There can always be errors like misspellings in the text you are tokenizing.
    
-   Size of memory of the device should be considered when loading textual files as there can always be files of massive scales.
    
-   Texts can be extracted from HTML and PDF. At times, it can be a daunting task. However, there are good modules that does the task efficiently and effectively
    
-   Unicode characters can be used as well. However, it is always better to decode them into a normalized form
    
-   Text could consist of names, dates, figures. Therefore, they should be handled well with respect to the potential machine learning model.
    

It is also kept in mind to assess the list of tokens after each stage of cleaning to avoid creating a mess and losing the ability to find where it originated. This is really important because regular expression-based filtering is used in the cleaning process.

  

## Conclusion
    

Cleaning is an integral stage in developing and training machine learning models related to language processing and other textual applications. Data pre-processing stage consists of tokenization, removing punctuation, case normalization, stop word removal, stemming, and lemmatization. The post-processing stages consist of text embedding and feature extraction. Text cleaning is highly a dependent and custom task that has no definite process. Therefore, it should be in the developer’s mind to have a thorough idea about how much the data should be cleaned and also how not to lose any important aspects of the texts during the process.
