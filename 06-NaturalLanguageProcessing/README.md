# Natural Language Processing



## Models

### Bag of Words Model

#### Preprocessing

Usually this would involve the following steps:

1. Removal of special characters
2. Change case for all words to lowercase
3. Do stemming and remove the words that don't matter
4. Do tokenization by using the following procedure

#### Procedure 

This is the most basic model for Natural Language Processing. It works as follows:

1. Select all distinct words and set them as columns of a matrix
2. Create as many rows as the number of observations
3. Each cell should now contain for each observation, the number of times the word appeared in it
4. Filter out other non-relevant words by setting a minimum frequency that a word must have across all observations in order for it to stay, 
5. Train this matrix for the classes available in a similar fashion to classification.

## Jargon

### Tokenization

Split all the different sentences into different words, each word gets a column which would contain the frequency of appearance of that word. This would be a sparse matrix that we would then operate upon it at will.

### Stemming

The process of collecting only the roots of words so that even if the same words appear in different forms, we always have a steady output and our machine learning models learn to recognize them properly and as the same words.

### Corpus

A corpus is a collection of texts of the same type.

### Sparsity 

The property that a matrix holding a lot of zeroes and very few values, is called sparsity.

## CODE REFERENCES

[1] **CountVectorizer**: It can be used to all the text cleaning necessary for the Bag of Words model, instead of having do to it manually. Read [documentation](http://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.CountVectorizer.html) for more.