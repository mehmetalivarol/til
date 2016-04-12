# Cheat Sheet of Useful Pandas Idioms

## Processing Data

Keep only the first two columns in a dataframe

```python
df= df.ix[:,:2]
```

Keep several groups of columns in a dataframe

```python
df1 = df[list(df.columns[0:1]) + list(df.columns[10:131])]
```

## Aggregating Data


###Get distinct counts of all columns in dataframe:

```python
for column in df:
    print column, df[column].nunique()
```
### Send column names to a list

```python
columns = df.columns.tolist()
```

## Selecting Data

Selecting specific index value (instead of by position)

```python
df1.loc[df1.index == '11/000,028']
```

or 

```python
df3.loc['11/000,028']
```



## Statistical Methods

Pairwise correlation of discrete or continuous variables [(methods pearson, kendall, spearman available)](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.corr.html)

```python
df.corr(method='pearson')["column"]
```

## Charting Data

### Histogram of non-numeric data

```python
histo = df.groupby('column').size()
plt.figure();
histo.plot.bar(); plt.axhline(0, color='k')
```

### Histogram of all columns in DF, regardless of numeric values

```python
for colname in df: 
    histo = df.groupby(colname).size()
    plt.figure();
    histo.plot.bar(); plt.axhline(0, color='k')
```
