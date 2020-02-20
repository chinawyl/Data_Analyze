一、DataFrame对象既有行索引，又有列索引

行索引，表明不同行，横向索引，叫index，0轴，axis=0

列索引，表名不同列，纵向索引，叫columns，1轴，axis=1

二、DataFrame常用属性和方法

![001](D:\Data_Analyze\pandas\dataframe\001.png)

三、还有更多的经过pandas优化过的选择方式

1.df.loc 通过**标签**索引行数据

2.df.iloc 通过**位置**获取行数据

四、pandas之布尔索引

![002](D:\Data_Analyze\pandas\dataframe\002.png)

注：

1.不同的条件需要括号括起来

2.&:且，|:或

五、pandas之字符串方法

![003](D:\Data_Analyze\pandas\dataframe\003.png)

六、缺失数据的处理

1.判断数据是否为NaN：pd.isnull(df),pd.notnull(df)

2.处理方式

处理方式1：删除NaN所在的行列dropna (axis=0, how='any', inplace=False)

处理方式2：填充数据，t.fillna(t.mean()),t.fiallna(t.median()),t.fillna(0)

3.处理0

处理为0的数据：t[t==0]=np.nan

当然并不是每次为0的数据都需要处理

计算平均值等情况，nan是不参与计算的，但是0会