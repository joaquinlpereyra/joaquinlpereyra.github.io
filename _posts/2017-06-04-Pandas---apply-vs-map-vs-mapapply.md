---
layout: post
title: Pandas - apply vs map vs mapapply
date: 2017-06-04 17:00:39
categories: pandas  python
---

Pandas provides three very useful function to apply functions to its dataframes
and series: apply, map and applymap. As I just started learning about Pandas and Numpy,
I often get confused and have to run to the documentation to remind me of which does what.

This should serve me as a quick reminder of what each one does. Hopefully it is useful for you too!

You should note the types are anotated in a Haskell-like[1] manner. If this confuses you, just ignore
it and go straight to the example.

## Apply

```python
# DataFrame x -> (x -> y) -> DataFrame y
# will apply the function f to each one of the columns of the dataframe
# and return a new dataframe with the headers as index and the ss
# series as the value of each of the new indexes

import numpy as np
from pandas import DataFrame, Series

people = ["I", "Lais", "May"]
plants = {2016: Series([0, 0, 7], index=people), 2017: Series([7, 0, 12], index=people)}

plants = DataFrame(plants)
print(plants)
#       2016  2017
# I        0     7
# Lais     0     0
# May      7    12
mean = plants.apply(np.mean)
print(mean)

# 2016    2.333333
# 2017    6.333333
# dtype: float64
```

## Map
```python
# Series x -> (x -> y) -> Series y
# will execute the function that goes from (x -> y) to each of the values of
# the series holding the values of type x and return a new series holding
# values of type y.

import numpy as np
from pandas import DataFrame, Series

people = ["I", "Lais", "May"]
plants = {2016: Series([0, 0, 7], index=people), 2017: Series([7, 0, 12], index=people)}

plants = DataFrame(plants)
print(plants)
#       2016  2017
# I        0     7
# Lais     0     0
# May      7    12

had_plants_in_2016 = plants[2016].map(lambda n: n > 0)
print(had_plants_in_2016)
# I       False
# Lais    False
# May      True
# Name: 2016, dtype: bool
```

## Applymap

```python
# Dataframe x -> (x -> y) -> Dataframe y
# very similar to map, but works for dataframes, not only Series

import numpy as np
from pandas import DataFrame, Series

people = ["I", "Lais", "May"]
plants = {2016: Series([0, 0, 7], index=people), 2017: Series([7, 0, 12], index=people)}

plants = DataFrame(plants)
print(plants)
#       2016  2017
# I        0     7
# Lais     0     0
# May      7    12

has_plants = plants.applymap(lambda n: n > 0)
print(has_plants)
#        2016   2017
# I     False   True
# Lais  False  False
# May    True   True
```
