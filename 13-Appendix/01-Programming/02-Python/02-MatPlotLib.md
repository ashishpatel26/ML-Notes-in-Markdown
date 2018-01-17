# MatPlotLib

This is the visualization library available for plotting graphs in python. It can be imported in any python script as ` import matplotlib.pyplot as plt`. This allows us to use the shorthand notation `plt` rather than having to use the complete name for the plot function.

## Plots

### Line based plot

```
# For graphs with lines
plt.plot(x, y)
plt.show()
```

### Scatter Plots

```
# For scatter plots
plt.scatter(x, y)
plt.show()
```

### Histograms

```
# bins = 10 by default and it corresponds to 
# the number of bins required
plt.hist(x, bins = 3)
plt.show()
```

### Plotting a DataFrame

A pandas DataFrame can be plotted using the `plt.plot(pd_df)` function. This call would plot all the numeric values in the dataframe across the index. 

### Customizations

1. **Labels**:The customizations for a plot `plt.plot(x,y)` for X and Y **labels** can be done with `plt.xlabel('X')` and `plt.ylabel('Y')`. 
2. **Title**: A title can be added with `plt.title('Plot Title')`.
3. **Altering Axis**: The axis' can be changed by passing an one dimensional array to the `yticks` function as in `plt.yticks([0,2,4,6])`. This would force the Y axis to have these numbers of the intervals. Optionally, a second list of the same length can also be passed to `yticks` for custom labels, while still using the first row as the original axis numbers. It can be done as  `plt.yticks([0,2,4,6],["Zero", "Two", "Four", "Six"])`.
4. **Adding Text**: Text can be added to any point in the plot using `plt.text(x, y, "Text")` syntax.
5. **Logarithms**: If the values are interfering with each other due to dominant behavior of a particular feature, then we can use `plt.yscale('log')` to neutralize the effect of that feature before showing the plot. 
6. **Colors**: Colors can be added for features while plotting them using `pd_df["column_1"].plot(color = "r")`.

## Exporting plots

We can easily export plots using `plt.savefig('filename.jpg')` before calling `show()` and save the plots.