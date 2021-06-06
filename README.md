bettersql -- A better SQL engine for DataFrames, Lists and Dictionaries
=====================================

[![Current version on PyPI](http://img.shields.io/pypi/v/bettersql.svg)][pypi]
[![Say Thanks!](https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg)](https://saythanks.io/to/joey@me.com)

Motivation
----------

Pandasql is a great project but it lacked the ability to call Python UDF's or use SQL to update a DataFrame. 
Bettersql allows both of these features plus there is no need to define a lambda to pass *globals()* because
I wrote the function to automatically get *globals()* from the caller level.

Installation
------------

To install bettersql, simply:

```console
$ pip install bettersql
```

Usage
-----

A simple example:

```python
import pandas as pd
from pandas import read_sql_query, DataFrame
from bettersql import sqldf

def reverse(x):
    # sample function with one parameter
    if x is not None:
        return x[::-1]
# DataFrame source
names = pd.DataFrame({'id':[1, 2, 3], 'name':['Alpha', 'Beta', 'Gamma'], 'category':[1, 2, 2]})    

# Dict of lists source
categories = {'id':[1, 2, 3], 'name':['One', 'Two', 'Three']}

sql = '''
SELECT n.id, n.name, n.category, c.name as categoryname, reverse(n.name) as reverse
FROM names AS n
LEFT JOIN categories AS c on n.category= c.id
'''

r = sqldf(sql, reverse = reverse) 
print(r)
```

