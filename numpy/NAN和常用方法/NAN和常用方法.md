一、nan性质

1.两个nan是不同的

```python
np.nan == np.nan #False
```

2.np.count_nonzero()

```python
np.count_nonzero(a) #判断非0数个数

np.count_nonzero(a!=a) #判断nan个数，依赖于第一个性质
```

3.np.isnan()

```python
a
array([[ 1.,  2.,  3.,  4.,  5.,  6.],
       [ 7.,  8.,  9., 10., 11., 12.],
       [13., 14., 15., 16., 17., 18.],
       [19., 20., 21., 22., nan, 24.]])

np.isnan(a) #判断是否有nan
array([[False, False, False, False, False, False],
       [False, False, False, False, False, False],
       [False, False, False, False, False, False],
       [False, False, False, False,  True, False]])
```

4.nan和任何数计算都是nan

```python
np.sum(a) #nan
```

二、nan常用统计函数

求和：t.sum(axis=None)

均值：t.mean(a,axis=None)  受离群点的影响较大

中值：np.median(t,axis=None) 

最大值：t.max(axis=None) 

最小值：t.min(axis=None)

极值：np.ptp(t,axis=None) 即最大值和最小值只差

标准差：t.std(axis=None) 



注:若将nan全部替换为0后，替换之前的平均值如果大于0，替换之后的均值肯定会变小，所以更一般的方式是把缺失的数值替换为均值（中值）或者是直接删除有缺失值的一行

```python
b.sum(axis=0) #axis= 0 对a的横轴进行操作，在运算的过程中其运算的方向表现为纵向运算

b.sum(axis=1) #axis= 1 对a的纵轴进行操作，在运算的过程中其运算的方向表现为横向运算
```

三、numpy的nan数据处理

```python
import numpy as np

def Change_Nan(a):
    for i in range(a.shape[1]): #遍历每一列
        temp_col = a[:,i] #当前这一列
        nan_number = np.count_nonzero(temp_col!=temp_col) #判断当前列是否有nan
        if nan_number != 0:
            temp_not_nan_col = temp_col[temp_col==temp_col]
            temp_col[np.isnan(temp_col)] = temp_not_nan_col.mean()
            
    return a
a = np.arange(24).reshape(4,6).astype(float)
a[1,2:] = np.nan
print(a)
print()
Change_Nan(a)
print(a)

[[ 0.  1.  2.  3.  4.  5.]
 [ 6.  7. nan nan nan nan]
 [12. 13. 14. 15. 16. 17.]
 [18. 19. 20. 21. 22. 23.]]

[[ 0.  1.  2.  3.  4.  5.]
 [ 6.  7. 12. 13. 14. 15.]
 [12. 13. 14. 15. 16. 17.]
 [18. 19. 20. 21. 22. 23.]]
```

