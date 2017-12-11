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

The algorithm treats each feature in the input data to be independent from each other. 