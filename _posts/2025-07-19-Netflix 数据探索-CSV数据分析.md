# Netflix 数据探索-CSV数据分析

数据来源

[Netflix Movies and TV Shows Dataset](https://www.kaggle.com/shivamb/netflix-shows )

### 1.读取数据

~~~python
```python
import pandas as pd
import matplotlib.pyplot as plt  # matplotlib是核心绘图库
import seaborn as sns #seaborn 也是绘图库，配色优于matplotlib
df=pd.read_csv("data/netflix_mini.csv") #填写下载来的csv存放地址
df.head() #读取数据
```
~~~

![](/images/post/netflix_ana/duqu)

### 2.数据简单清洗

```python
print(df.info())  # 查看缺失值
# 填补或删除缺失值
 df = df.dropna(subset=["director"])  #删除没有导演的数据

```

> [!NOTE]
>
> 关于如何处理缺失值，有很多种方法，要按照不同的情况选择合理的方法,随后再讨论。



### 2.基础分析

```python
print("记录总数：",len(df))
print("电影数量：",sum(df['type']=="Movie"))
print("剧集数量：",sum(df['type']=="TV Show"))
print("发行年份：\n",df['release_year'].value_counts().sort_index())

```

```
记录总数： 6
电影数量： 4
剧集数量： 2
发行年份：
 release_year
2017    1
2018    1
2019    2
2020    1
2021    1
Name: count, dtype: int64
```



### 3.可视化

```python
sns.countplot(data=df,x="type",palette="Set2") #Set2柔和配色 横轴为类型
plt.title("Movies vs TV Shows")#表头内容
plt.show()
```

![](/images/post/netflix_ana/output_2_1.png)

```python
#发行年份趋势
df["release_year"].value_counts().sort_index().plot(kind="line",marker="o")#类型是折线图，数据在图中用圆点表示
plt.title("发行年份趋势")
plt.xlabel("Year") #横轴为年份
plt.ylabel("Count")#纵轴为数量
plt.show()
```

![](/images/post/netflix_ana/output_3_1.png)

> [!TIP]
>
> 绘图完成后发现表头内容不显示文字而是显示了矩形方框，是因为**matplotlib 默认不支持中文字体**，所以图表里汉字会显示成方块或者乱码。
>
> 解决方案：
>
> ```python
> #在代码中加入
> import matplotlib.pyplot as plt
> plt.rcParams['font.family'] = 'SimHei'  # 设置中文为黑体
> plt.rcParams['axes.unicode_minus'] = False  # 解决负号显示问题
> ```
>
> 

```python
#前5国家
df['country'].value_counts().head(5).plot(kind="bar")#绘图类型为柱状图
plt.title("TOP 5")
plt.ylabel("Count") #纵轴为横轴对应的国家发行总数量
plt.show()
```

![](/images/post/netflix_ana/output_4_0.png)

### 4.导出数据

```python
#导出清洗后的数据
df.to_csv("netflix_cleaned.csv",index=False)
print("已保存为netflix_cleaned.csv")
```

