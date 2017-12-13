# Classification

1. [Logistic Regression](./01-LogisticRegression.md)
2. [K-Nearest Neighbours](./02-knn.md)
3. [Support Vector Machines](./03-SupportVectorMachines.md)
4. [Naive Bayes](./04-NaiveBayes.md)
5. [Decision Tree Classification](./05-DecisionTree.md)
6. [Random Forest Classification](./06-RandomForest.md)

## Types of Classification Algorithms

1. **Discriminative Learning Algorithms** 
	
	These algorithms try to learn the probability of an end result **Y** for a given feature set **X**. These algorithms try to determine how **Y** is directly a function of **X**. Mathematically these are shown as 
	
	![pyx](http://mathurl.com/cqd6fro.png)
	
	Some of these algorithms try to learn a hypothesis that tries to predict the possible classes, mathematically represented as 
	
	![binarhypothesis](http://mathurl.com/ya46sgrc.png)
	
2. **Generative Learning Algorithms**

	This type of Algorithms try to learn, the probability of a given set of features **X** for a particular class **Y** (mathematically represented as ![pxy](http://mathurl.com/bwse6yv.png)) and also, the probability of occurrence of this class **Y** (the probability of occurrence of a given class is represented as ![py](http://mathurl.com/byg852g.png) and is called **class prior**. The most popular example of such algorithms is the [Naive Bayes Algorithm](./04-NaiveBayes.md).