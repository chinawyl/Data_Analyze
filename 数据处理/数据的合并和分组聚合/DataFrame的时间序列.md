一、pd.date_range(start=None, end=None, periods=None, freq='D')

注:

1.start和end以及freq配合能够生成start和end范围内以频率freq的一组时间索引

2.start和periods以及freq配合能够生成从start开始的频率为freq的periods个时间索引

![003](D:\Data_Analyze\数据处理\数据的合并和分组聚合\003.png)二、转换pandas时间类型与重采样

重采样：指的是将时间序列从一个频率转化为另一个频率进行处理的过程，将高频率数据转化为低频率数据为降采样，低频率转化为高频率为升采样

![004](D:\Data_Analyze\数据处理\数据的合并和分组聚合\004.png)

```python
df["timeStamp"] = pd.to_datetime(df["timeStamp"])
df.set_index("timeStamp",inplace=True)

count_month = df.resample("M").count()["title"]
```

三、时间戳和时间段

DatetimeIndex:时间戳

PeriodIndex:时间段

```python
#转换为时间段
period = pd.PeriodIndex(year=df["year"],month=df["month"],day=df["day"],hour=df["hour"],freq="H")

#时间段降采样
df = df.set_index(period).resample("10D").mean()

```



和

periods

以及

freq

配合能够生成从

start

开始的频率为

freq

的

periods

个

时间索