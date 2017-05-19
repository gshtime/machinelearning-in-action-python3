# 勘误
## P22页

命令 datingDataMat,datingLabels=kNN.file2matrix('datingTestSet.txt')要改为datingDataMat,datingLabels=kNN.file2matrix('datingTestSet2.txt')，不然会出现错误

> ValueError: invalid literal for int() with base 10: 'largeDoses'

# 部分函数说明

## numpy.tile()函数

函数格式tile(A,reps)

A和reps都是array_like

A的类型众多，几乎所有类型都可以：array, list, tuple, dict, matrix以及基本数据类型int, string, float以及bool类型。

reps的类型也很多，可以是tuple，list, dict, array, int, bool.但不可以是float, string, matrix类型。

reps的数字从后往前分别对应A的第N个维度的重复次数。如tile（A,2）表示A的第一个维度重复2遍，tile（A,(2,3)）表示A的第一个维度重复3遍，然后第二个维度重复2遍，tile（A,(2,2,3)）表示A的第一个维度重复3遍，第二个维度重复2遍，第三个维度重复2遍。

## operator.itemgetter函数
operator模块提供的itemgetter函数用于获取对象的哪些维的数据，参数为一些序号（即需要获取的数据在对象中的序号），下面看例子。

```
>>> a = [1,2,3] 
>>> b=operator.itemgetter(1)   //定义函数b，获取对象的第1个域的值
>>> b(a) 
2 
>>> b=operator.itemgetter(1,0)  //定义函数b，获取对象的第1个域和第0个的值
>>> b(a) 
(2, 1)
```

要注意，operator.itemgetter函数获取的不是值，而是定义了一个函数，通过该函数作用到对象上才能获取值。

## sorted()函数

Python内置的排序函数sorted可以对list或者iterator进行排序，官网文档见：[官方文档：sorted()](http://docs.python.org/2/library/functions.html?highlight=sorted#sorted)，该函数原型为：

> sorted(iterable[, cmp[, key[, reverse]]])

### 参数解释

（1）iterable指定要排序的list或者iterable，不用多说；

（2）cmp为函数，指定排序时进行比较的函数，可以指定一个函数或者lambda函数，如：

students为类对象的list，没个成员有三个域，用sorted进行比较时可以自己定cmp函数，例如这里要通过比较第三个数据成员来排序，代码可以这样写：
```
>>> students = [('john', 'A', 15), ('jane', 'B', 12), ('dave', 'B', 10)]
>>> sorted(students, key=lambda student : student[2])
```

（3）key为函数，指定取待排序元素的哪一项进行排序，函数用上面的例子来说明，代码如下：

```
>>> sorted(students, key=lambda student : student[2])
```

key指定的lambda函数功能是指定student列表的第三个域（即：student[2]），因此sorted排序时，会以students所有元素的第三个域来进行排序。

有了上面的operator.itemgetter函数，也可以用该函数来实现，例如要通过student的第三个域排序，可以这么写：
```
>>> sorted(students, key=operator.itemgetter(2)) 
```
sorted函数也可以进行多级排序，例如要根据第二个域和第三个域进行排序，可以这么写：
```
>>> sorted(students, key=operator.itemgetter(1,2))
```
即先跟句第二个域排序，再根据第三个域排序。

（4）reverse参数就不用多说了，是一个bool变量，表示升序还是降序排列，默认为false（升序排列），定义为True时将按降序排列。

sorted()的更多例子见：[更多例子](https://wiki.python.org/moin/HowTo/Sorting/)

## sum()函数

成员函数sum(axis=1)，axis=1 表示每行相加，得到一个列