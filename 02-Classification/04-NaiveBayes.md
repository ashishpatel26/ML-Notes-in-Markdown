# Naive Bayes

## Intuition

The Naive Bayes classifier works on Bayes Theorem.

### Bayes Theorem

The Bayes' Theorem suggests that it is possible to calculate the probability of occurence of some event, based upon the previous knowledge of something else having occurred already. This idea generalizes the concept of **conditional probability**. The following formula allows us to calculate the conditional probability:

![bayes](http://mathurl.com/yd5wgr73.png)

where:

![ph](http://mathurl.com/ydeqdel2.png) is the probability of hypthesis H being true

![pe](http://mathurl.com/y85hwz3k.png) is the probability of event E regardless of H

![peh](http://mathurl.com/ycu2debl.png) is the probability of event E provided that H is true

![phe](http://mathurl.com/y6wymudv.png) is the probability of hypothesis H being true provided that event E has occurred. 

## NB-Classifier Algorithm

This is supervised machine learning classifier because we'll be classifying things on the basis of previous information provided to us. The algorithm treats each feature in the input data to be independent from each other which could be a setback in some cases, and is the reason why its called **Naive Bayes**. The fundamental assumption, that all variables are independent, can be wrong and even then it's applied and gives decent result. 

### Structure

The equation would become something like this for finding the probability that a particular set of features **X** corresponds to the class, **Class 1**:

![bayesml](http://mathurl.com/y7c6qgbp.png)

where the notations used are as follows:

1. ![priorprob](http://mathurl.com/y76nhwxz.png) is called **prior probability**
2. ![marginallikelihood](http://mathurl.com/ycd77fxh.png) is called **marginal likelihood**
3. ![likelihood](http://mathurl.com/y7l54x5t.png) is called **likelihood**
4. ![posteriorprob](http://mathurl.com/yaenwjzj.png) is called the **posterior probability**

and are usually calculated in that order.

### Procedure 

1. The procedure for calculating ![priorprob](http://mathurl.com/y76nhwxz.png) is pretty straight forward. We take the number of occurrences of **Class 1** and divide it by the total number of observations in our dataset. Therefore

	![priorprobformula](http://mathurl.com/yckqgn5y.png) 

2. The calculation of ![marginallikelihood](http://mathurl.com/ycd77fxh.png) is dependent on the choice made by the user as well. The following steps need to be performed for calculation of marginal likelihood:
	1. We define an n-dimensional **proximity range** in the feature space with a radius/width/span of **r**
	2. Then we are going to look at all the points that are enclosed in the range
	3. These points will now be deemed similar to the new data point that needs to be classified.
	4. The marginal likelihood ![marginallikelihood](http://mathurl.com/ycd77fxh.png) is therefore the probability of any new random point being added to fall into this range that we just selected given by

	![marginallikelihoodformula](http://mathurl.com/y8s9mo57.png)
	
3. ![likelihood](http://mathurl.com/y7l54x5t.png) represents the likelihood of an observation that belongs to **Class 1** exhibiting the **Feature Set X**. 
	
	1. We define an n-dimensional **proximity range** in the feature space with a radius/width/span of **r**
	2. Then we are going to look at all the points that are enclosed in the range
	3. These points will now be deemed similar to the new data point that needs to be classified.
	4. The probability that needs to be calculated is the probability that a randomly selected datapoint will be within the **proximity range**, provided that we know that it already belongs to **Class 1**. From here, this become pretty straight forward to calculate and is given by
	
	![likelihoodformula](http://mathurl.com/yd4pdpnw.png)

### Types

1. **Multinomial NB**: This type of algorithm is usually used for counts like classification problems in NLP
2. **Gaussian NB**: Details to go here. 
	

### Advantages

1. Simple to build and quite intuitive
2. Easily trained upon small datasets
3. Works fast once trained and even the training time is not too much
4. Not very sensitive to irrelevant features
5. Since it works on probabilities and has one underlying bias, it can often make correct classification in scenarios where SVM or K-NN aren't very useful because they're linear classifiers.

### Disadvantages

1. Assumption that every feature is independent, which is rarely the case. 

