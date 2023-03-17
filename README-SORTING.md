

## Finding sorting algorithm

Some high-level comments [here](https://stackoverflow.com/questions/44205655/sorting-algorithm-used-by-pandas-sort-values-when-the-kind-parameter-is-not-app).
[`get_group_index_sorter`](https://github.com/sebawild/pandas/blob/main/pandas/core/sorting.py#L630)
seems to be the main decision point: it either does numpy's mergesort or some counting sort

The docs for `DataFrame.sort_values` points to this source:
https://github.com/pandas-dev/pandas/blob/v1.5.3/pandas/core/frame.py#L6862-L6942

which in turn calls methods from this file:
https://github.com/pandas-dev/pandas/blob/main/pandas/core/sorting.py


Note that `DataFrame` also has a method [`sort_index`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.sort_index.html);
this one sorts by the index labels.
We may want to accept both methods as “sorting”.
`sort_index` calls the superclass implementation in `generic.py`, which 
delegates teh work to [`get_indexer_indexer`](https://github.com/pandas-dev/pandas/blob/2e218d10984e9919f0296931d92ea851c6a6faf5/pandas/core/sorting.py#L52)


Key sorting methods:
* [`lexsort_indexer`](https://github.com/pandas-dev/pandas/blob/main/pandas/core/sorting.py#L304):

   
