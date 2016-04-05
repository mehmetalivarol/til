# Cheat Sheet of Useful Pandas Idioms

## Processing Data

Keep only the first two columns in a dataframe

```python
df= df.ix[:,:2]
```

## Aggregating Data


###Get distinct counts of all columns in dataframe:

```python
for column in df:
    print column, df[column].nunique()
```

## Charting Data

### Histogram of non-numeric data

```python
histo = df.groupby('column').size()
plt.figure();
histo.plot.bar(); plt.axhline(0, color='k')
```
