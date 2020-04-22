### 本实验所有使用数据存放在压缩包，文件数据路径请自行更改

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

十四、pandas的series索引

```python
x[[2,3,6]]
x[["C","E","G","I"]]

#连续多个值(普通切片，左闭右开)
print(x[0:4])
print("*"*100)

#连续多个值(标签切片，左闭右闭)
print(x["A":"E"])
print("*"*100)

A    0
B    1
C    2
D    3
dtype: int64
****************************************************************************************
A    0
B    1
C    2
D    3
E    4
dtype: int64
****************************************************************************************

#获取index和value不用加括号
print(x.index,type(x.index))
print(x.values,type(x.values))
```

十五、pandas的dataframe两种字典写法

```python
d1 = {"name":["ztfl","xyql","scsyl"],"age":[20,26,26],"tel":[10086,138830,139839]}

d2 = [{"name":"ztfl","age":20,"tel":10086},{"name":"xyql","age":26},{"name":"scsyl","tel":139839}]
```

十六、dataframe取数据

1.loc和iloc后面是[]不是()

2.:用符号取包括右边，数字取不包括

```python
#df.loc 通过标签索引行列数据
t.loc["a","Z"]
t.loc["a":"c",["W","Z"]] #冒号是闭合的，包括冒号后面的数据
```

3.dataframe不加loc和iloc只能取行或列

```python
df[:20] #写数字表示取行

df["Row_Labels"] #写字符串，取列

#t字符串
W	X	Y	Z
a	0	1	2	3
b	4	5	6	7
c	8	9	10	11

t["a"]会报错
取单行t[0]会报错，要写成t[0:1]
```

4.连续或不连续

```python
#不连续的行列
t.iloc[[0,2],[2,1]]
#连续的行列
t.iloc[1:,:2]

#自动转换为nan，不需要转换为float
t.iloc[1:,:2] = np.NAN
```

十七、dataframe多个条件用&或|，且每个条件要加()

```python
clean = df[(df["Row_Labels"].str.len()>4)&(df["Count_AnimalName"]>700)]
```

十八、dataframe排序和常用属性方法

```python
df = df.sort_values(by="Count_AnimalName",ascending=False) #False为倒序

属性记得加()
df.info()
df.describe()
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

二十、取值要用values，否则有坐标，且不用加()

```python
print(df["Runtime (Minutes)"])
0      121
1      124
2      117
3      108
4      123
5      103
6      128
7       89
8      141
9      116
10     133
11     127
12     133
13     107
14     109
15      87
16     139
17     123
18     118
19     116
20     120
21     137
22     108
23      92
24     120
25      83
26     159
27      99
28     100
29     115
      ... 
970     92
971    105
972    123
973    111
974    124
975     94
976    113
977     92
978     97
979    120
980    109
981    118
982    133
983    104
984    111
985    102
986     92
987    104
988     99
989    128
990     92
991    165
992     97
993     97
994     88
995    111
996     94
997     98
998     93
999     87
Name: Runtime (Minutes), Length: 1000, dtype: int64

即print(df["Runtime (Minutes)"].values)
```

二十一、求某列长度

```python
#导演人数
print(len(set(df["Director"].tolist())))
print(len(df["Director"].unique())) #unique直接转换为列表，且唯一

#演员人数
temp_actor_list = df["Actors"].str.split(",").tolist()
actor_list = [i for j in temp_actor_list for i in j ]
actor_numbers = len(set(actor_list))
```

二十二、多个条件分组聚合

```python
grouped1 = df["Brand"].groupby(by=[df["Country"],df["State/Province"]]).count() ##返回Series
grouped2 = df.groupby(by=[df["Country"],df["State/Province"]])[["Brand"]].count() #返回DataFrame
grouped3 = df.groupby(by=[df["Country"],df["State/Province"]]).count()[["Brand"]] #返回DataFrame
```

二十三、DataFrame设置复合索引加[]

```python
df.set_index(["W","X"])

		Y	Z
W	X		
0	1	2	3
4	5	6	7
8	9	10	11

df.set_index(["W","X"]).index

MultiIndex(levels=[[0, 4, 8], [1, 5, 9]],
           codes=[[0, 1, 2], [0, 1, 2]],
           names=['W', 'X'])
```

