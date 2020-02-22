一、dtype是属性，不是方法，不用加()

```python
a.dtype
```

二、random有()

```python
g = np.array([random.random() for i in range(10)])
```

三、shape没有()，有也是[]

```python
a.shape[1]
```

四、numpy数组运算遵守广播原则

五、numpy中取行列

```python
#只取行时不用写列，但只取列时要写行
t[1] #第二行
t[:,1] #第二列

#取不连续的行或列时用[]，且从0开始
t[[3,7,9]] #取第4,8,10行
t[:,[1,4,6]] #取第2,5,7列

#取不连续的行列时得到的是多个不相邻的点
t2[[0,2],[0,1]] #(0,0)和(2,1)
```

六、t[t<10]等价于t = [t<10]

七、numpy中的clip函数为

```python
numpy.clip(a, a_min, a_max, out=None)[source] 
#clip函数将数组中的元素大于a_max的就使得它等于a_max，小于a_min,的就使得它等于a_min，不在范围内的不变
```

八、np.zeros()和np.ones()输入行列时需要再打一个()

```python
np.zeros((us_data.shape[0],2)).astype(int)
```

九、vstack()和hstack()都要加()

```python
np.vstack((us_data,uk_data))
```

十、行交换或者列交换只用把索引顺序交换就行

```python
#行交换
final_data[[1,2],:] = final_data[[2,1],:] 

# 列交换
final_data[:,[0,2]] = final_data[:,[2,0]]
```

十一、numpy中np.nan必须是float型

十二、numpy中sum

```python
b.sum(axis=0) #axis= 0 对a的横轴进行操作，在运算的过程中其运算的方向表现为纵向运算

b.sum(axis=1) #axis= 1 对a的纵轴进行操作，在运算的过程中其运算的方向表现为横向运算
```

十三、pandas的series有index

```python
f = pd.Series([1,2,34,74,6,4],index=list("abcdef"))  #索引和值个数要相同
```

十四、pandas的series取多个值加个[]

```python
x[[2,3,6]]
x[["C","E","G","I"]]
```

十五、pandas的dataframe两种字典写法

```python
d1 = {"name":["ztfl","xyql","scsyl"],"age":[20,26,26],"tel":[10086,138830,139839]}

d2 = [{"name":"ztfl","age":20,"tel":10086},{"name":"xyql","age":26},{"name":"scsyl","tel":139839}]
```

十六、dataframe取数据

```python
df[:20] #写数字表示取行

df["Row_Labels"] #写字符串，取列

#df.loc 通过标签索引行列数据
t.loc["a","Z"]
t.loc["a":"c",["W","Z"]] #loc的冒号是闭合的，包括冒号后面的数据

#df.iloc 通过位置获取行数据
#不连续的行列
t.iloc[[0,2],[2,1]]
#连续的行列
t.iloc[1:,:2]

#自动转换为nan，不需要转换为float
t.iloc[1:,:2] = np.NAN
```

十七、dataframe多个条件用&或|

```python
clean = df[(df["Row_Labels"].str.len()>4)&(df["Count_AnimalName"]>700)]
```

十八、dataframe排序

```python
df = df.sort_values(by="Count_AnimalName",ascending=False) #False为倒序
```

十九、dataframe缺失值处理

```python
#缺失值方法处理一:删除NaN
t1.dropna(axis=0,how='any',inplace=True) 
#how默认为any(只要存在NaN就会删除，而all是全为NaN删除),inpleace默认为False(Trun为直接修改原值)

#缺失值方法处理二:用平均数填充
t2.fillna(t2.mean()) #也可以单独填充某一列
```

注:pandas的nan不参与计算