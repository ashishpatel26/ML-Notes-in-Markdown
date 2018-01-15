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

### Customizations

1. The customizations for a plot `plt.plot(x,y)` for X and Y **labels** can be done with `plt.xlabel('X')` and `plt.ylabel('Y')`. 
2. A **title** can be added with `plt.title('Plot Title')`.
3. The axis' can be changed by passing an one dimensional array to the `yticks` function as in `plt.yticks([0,2,4,6])`. This would force the Y axis to have these numbers of the intervals. Optionally, a second list of the same length can also be passed to `yticks` for custom labels, while still using the first row as the original axis numbers. It can be done as  `plt.yticks([0,2,4,6],["Zero", "Two", "Four", "Six"])`.
4. Text can be added to any point in the plot using `plt.text(x, y, "Text")` syntax.