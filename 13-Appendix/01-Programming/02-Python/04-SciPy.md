# SciPy

## Read and Import Data

### Matlab Files

We can read files from matlab using the `scipy.io.loadmat()` function as shown below

```python
import scipy.io

matlab_data = scipy.io.loadmat('filepath.mat')
```

This would create a dictionary object called `matlab_data` that would contain key value pairs for all the different kinds of objects that have been imported from the matlab file. 

> It is interesting to note here that Matlab files are usually permanently stored work environments of Matlab so multiple objects should be expected while importing a single matlab file. 