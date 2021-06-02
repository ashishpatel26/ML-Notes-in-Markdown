# Eclat

In the eclat model, we only have support. When we calculate the support, in an Eclat model, we are consider the prevalence of a set of items and not individual models. This makes sense because in case of Eclat models, since we only have support, the individual items is just the frequency of the items and nothing more than that.

![eq1](http://mathurl.com/y9g59dlu.png)

The algorithm, as one would intuitively assume it to, works as follows:

1. Set a minimum support
2. Select all subsets of transactions having support more than the minimum support
3. Sort these subsets by decreasing order of support

## CODE REFERENCES

* R is a better language for this algorithm as well
