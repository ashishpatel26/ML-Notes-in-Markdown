# Apriori

The Apriori algorithm has three parts titled **support**, **confidence** and **lift**. 

**Support**

The support for a movie M is defined by the following equation

![eq1](http://mathurl.com/y9g59dlu.png)

**Confidence**

The confidence is a metric calculated for any given pair of elements. We test rules using this method because it gives us an idea about what fraction of people who have watched M1, have also watched M2. In other words, how frequently do the two movies appear together in users' watchlist.

![eq2](http://mathurl.com/ybqbxvm2.png)

**Lift**

The lift is the confidence divided by support as shown in the following equation. It is the likelihood of a person liking M2, when they are chosen at random from another sample of the same distribution and have M1 in their watchlist. The higher the lift, the higher is the probability of a person who has watched M1 watching M2.

![eq3](http://mathurl.com/yasxs8o5.png)

The algorithm then proceeds in the following steps:

1. Set a minimum support and confidence, mainly due to immense number of combinations 
2. Take all subsets in the transactions having more support than the minimum support
3. Take all subsets in the transactions having more confidence than the minimum confidence
4. Sort the rules by decreasing order of lift

> It must be kept in mind that the values of Support, Life and Confidence may seem mathematical in the equations above, but are experimental in nature. We choose a value for the parameters, run some the algorithm and then change the value of those parameters and run the algorithm again. We base these values on the empirical data, i.e. the set of rules obtained in this example. 

## CODE REFERENCES

* It is interesting to note that the Apriori function that is used in Python does not expect a data frame, instead, expects a list of lists that contain various different transactions. This is quite natural as well, because a horizontal or vertical data frame does not make much sense when it is about business transactions or movies watched. The reason for this is, people have often watched different number of movies, read different number of books etcetera. Applying a rectangular structure on such data and then performing any manual operations upon the same would often cause a lot of data to be missing for it to make any sense or structure at all. 

* R is a better language for this algorithm
