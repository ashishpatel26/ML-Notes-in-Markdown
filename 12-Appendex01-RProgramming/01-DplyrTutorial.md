# Tutorial (dplyr)

Dplyr is perhaps the most commonly used data wrangling tool in R. In this section, we will be exploring some of the commonly used functions and writing styles of **dplyr**.

> The **dplyr** verbs do NOT change the original dataset, they only return modified copies for us to use. 

## Select

This dplyr verb allows us to select certain columns from the dataset. The syntax is straight forward.

```r
select(df, Column1, Column2)
```

There are few things that need to be taken care of during the usage of **select** verb.

1. No quotes required for column names
2. No **$** sign required in front of the column names
3. One can use numeric order of columns for select, i.e. `select(df, 2:5)` would select the column number **2** to **5** from the dataframe **df**
4. After selection, we can also select which columns to not choose from the dataset, by using a syntax like `select(df, 2:5, -(3:4))`. This command would choose the column **2** through **5** without the columns **3** through **4**.

> All verbs are compatible with helper functions described at the end of this documnet.

## Mutate

This dplyr verb allows us to add new variables to the dataset using the existing variables. 

```r
mutate(df, newCol = Col1 + Col2)
```

In the example above, a new column **newCol** would be created by adding the values already present in **Col1** and **Col2**. 

Again, no quotes or **$** signs are required in order to use mutate. Although, if there are spaces in the column name, such as a column with the name **Col 1** can be written with the help of wrapping the name in **`** instead of quotes.

## Filter

This verb allows us to filter out rows from the dataset based on the conditions that we provide as arguments to the verb. The syntax for filter is as intuitive as the other verbs.

```r
filter(df, Condition == 1)
```

where `df` is the tibble, followed by one or more logical tests after the **,**.

## Arrange

This verb allows us to reorder observations in a data frame so that they're easier to observe and visualize. The syntax for arrange is quite simple.

```r
arrange(df, ColumnToArrangeDataBy)
```


## Helper Functions

1. `starts_with("X")`: every name that starts with **X**
2. `ends_with("X")`: every name that ends with **X**
3. `contains("X")`: every name that contains **X**
4. `matches("X")`: every name that matches **X**, where **X** can be a regular expression
5. `num_range("x", 1:5)`: the variables named **x01**, **x02**, **x03**, **x04** and **x05**
6. `one_of(x)`: every name that appears in **x**, where **x** is a character vector.