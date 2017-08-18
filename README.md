# Machine-Learning-in-Action-Study
This repository includes resources of my study work on the book Machine Learning in Action.

# Wrong in book

## P41

程序清单3-4，语句

```python
del(labels(bestFeat))
```

破坏了labels的结构，需在后面for循环块之后，return语句之前进行恢复，即添加下述语句

```python
labels.insert(bestFeat, bestFeatLabel)
```

## P162
上部，`binSplitDataSet()`函数中代码

```python
mat0 = dataSet[nonzero(dataSet[:,feature] >value)[0], :][0]
mat1 = dataSet[nonzero(dataSet[:,feature]<=value)[0], :][0]
```

应改为

```python
mat0 = dataSet[nonzero(dataSet[:,feature] >value)[0], :]
mat1 = dataSet[nonzero(dataSet[:,feature]<=value)[0], :]
```

## P164

程序清单9-2，`chooseBestSplit`函数中代码

```python
for featIndex in range(n-1):
    for splitVal in set(dataSet[:,featIndex]):
```

应改为

```python
for featIndex in range(n-1):
    for splitVal in set(dataSet[:,featIndex].T.tolist()[0]):
```

# reDraw.rawDat[:,0].A，需要将矩阵转换成数组
reDraw.a.scatter(reDraw.rawDat[:,0].A, reDraw.rawDat[:,1].A, s=5)

## P186

程序清单10-1，`randCent`函数中代码
```python
centroids[:,j] = minJ + rangeJ * random.rand(k,1)
```

应改为

```python
centroids[:,j] = minJ + rangeJ * * random.random(size=(k,1))
```
