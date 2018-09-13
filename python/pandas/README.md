# Pandas

### Group by aggregation in python

```python
def agg_example(x):
    names = {'count': x['col'].count(),
             'unique': x['col'].nunique(),
             'sum': x['col'].sum()}
    return pd.Series(names, index = [key for key in names])

df.groupby(['col']).apply(agg_example).reset_index()
```

### Group by with percentage across group

```python
df['%'] = stats.groupby(['col'])['col'].apply(lambda x: x / float(x.sum()) * 100)
```

### Group by and sample

```python
df.groupby(['bbc_hid3'])['col'].apply(lambda x: x.sample(n = 1)).reset_index()
```

### Group by and rank

```python
df['rank'] = df.groupby(['col'])['col'].rank()
```

### Return multiple cols from an apply

```python
def func(x):
    a = x * 2
    b = x * 4
    return (a, b)

df[['a', 'b']] = df.apply(lambda x: pd.Series(func(x)), axis = 1)
```

### Pivot table with counts

```python
df.pivot_table(index = 'col', columns = 'col', values = 'col', aggfunc = 'count')
```

### Filter rows will all zeros

```python
df = df[(df.T != 0).any()]
```

