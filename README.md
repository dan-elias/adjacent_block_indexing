# Adjacent Block Indexing for Record Linkage


Summary
-------

The code in this repository is intended for use with the [recordlinkage](http://recordlinkage.readthedocs.io/en/latest/)
package.  It contains an implementation of the Adjacent Block Indexing method.  
This method combines some features of Standard Blocking, 
and Sorted Neighbourhood Indexing.  In addition, it also allows for
meaningful treatment of missing values and the simultaneous use of multiple
sorting orders for the blocks (ie: sorting by each of the blocking keys
individually).  

IPython Notebooks in this repo perform numerical experiments in which Adjacent Block
Indexing is compared to Standard Blocking and Sorted Neighbourhood Indexing.  These
take some time to run.  Their results are that *under the conditions tested*:

* Adjacent Block Indexing has similar scalability properties to Sorted Neighbourhood Indexing, Standard Blocking
and Full Indexing (ie: runtime is approximately linear with respect to the size of the 
index produced)
* Compared to the other methods, Adjacent Block Indexing can produce superior index 
quality at the expense of increased runtime.


Contents
--------

File                        | Description
----------------------------|----------------
adjacent_block_index.py     | Implementation of Adjacent Block Indexing (requires recordlinkage)
experiment_helpers.py       | Helpers used by the test scripts
index_quality.ipynb         | Notebook to run index quality test and display results
scalability.py              | Script to run scalability test
scalability_results.ipynb   | Notebook for viewing results of scalability test


Instructions
------------

To use Adjacent Block Indexing
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Use the AdjacentBlockIndex class in adjacent_block_index.py.  It has the same API
as indexers in recordlinkage.

To run the index quality test
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
In Jupyter, open index_quality.ipynb and run all cells


To run the scalability test
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Disable memory paging.  To do this on Linux, use:

```
sudo watch --interval 500 swapoff -a
```

Then, run scalability.py repeatedly until the file timings.pickle is created (until all tests are done, partial results are
saved to and recovered from _timings.pickle).  To do this on Linux, navigate the same directory
as scalability.py and then use:

```
while [ ! -f timings.pickle ]; do python scalability.py ; done
```

When this is complete, results can be viewed by opening scalability_results.ipynb in Jypyter and running all cells.




