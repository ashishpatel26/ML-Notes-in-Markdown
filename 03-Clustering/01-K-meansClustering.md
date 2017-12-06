# K-means Clustering

This is a classic clustering algorithm that relies on the concept of centroids and their Euclidean distances from the observed data points. The basic concept works on the following set of rules:

1. Assign a fixed number of centroids randomly in the parameter space (the number of centroids will define the number of clusters formed at the end of execution of the algorithm). These centroids need not be one of the points in the observation set, and can literally be random coordinates in the multi-dimensional space that we have.
2. Calculate the closest centroid from each data point in the observation set and assign the data point to that centroid's cluster.
3. Move the centroid to the 'center-of-mass' of the cluster that it has created with help of our data points from observation set.
4. Repeat **Step 2** and see if any points have changed their clusters, from the ones they were previously assigned. If the condition holds true then move to **Step 3** otherwise proceed to **Step 5**. 
5. Finish

Although, the algorithm might appear like its' construction of clusters based on the distances, this assumptions is untrue. The **k-means clustering algorithm works primarily on minimizing the intra-cluster variance** and that is the reason why metric of computation for accuracy of a k-means cluster is WCSS (within-cluster sum of squares).

> It is interesting to observe that the k-means clustering algorithm relies on Euclidean distances for formation of clusters and computation of intra-cluster variation. This is an implicit underlying bias of the algorithm and can be exploited for other kinds of correlations between the attributes by transforming them into Euclidean distances. Click here for a more detailed explanation regarding this. 

**Drawbacks**: As it should be already obvious at this point, the selection of random points could cause serious problems because this randomness would let the Algorithm figure out different clusters than the ones that are actually present in the hyper-dimensional space.  This problem has been alleviated to some extent by the use of k-means++algorithm. 

##RESEARCH ARTICLES

1.  **K-Means++** : The advantages of careful seeding

	**[Solved]** The random selection of centroids would often let the k-means algorithm figure out different clusters than the ones that are actually present in the hyper-dimensional space.
	
	This algorithm selects only the first centroid at random and then picks the remaining centroids by using a probability distribution function over the data points.  (**Section 2.2** of [David Arthur and Sergei Vassilvitskii](http://ilpubs.stanford.edu:8090/778/1/2006-13.pdf)) 


##CODE REFERENCES

Read the [documentation](http://scikit-learn.org/stable/modules/generated/sklearn.cluster.KMeans.html) for more 
