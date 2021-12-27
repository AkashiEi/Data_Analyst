# 个人Pandas常用功能合集~持续更新（大概）

###  **导入依赖库**   


```python
import pandas as pd
```

##### 关掉warning


```python
import warnings
warnings.filterwarnings("ignore")
```

### **读取数据**  
#### **读取csv、txt文件**  
`pd.read_csv(文件名, sep=·分隔符，默认是','·, header=·第几行开始读取，默认0·,encoding=·编码格式，默认utf8·)
`     
#### **读取xls、xlsx文件**  
`pd.read_excel(文件名, sheet_name=·sheet名/序号（从0开始），默认第一个，若填写None时会全读取,，但返回的将是字典格式·)
` 


```python
df0 = pd.read_excel('Desktop/test_data.xlsx',sheet_name='主机游戏')
df0
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>游戏名</th>
      <th>游玩时长(h)</th>
      <th>发布时间</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>塞尔达传说 旷野之息</td>
      <td>600</td>
      <td>2017-03-03</td>
    </tr>
    <tr>
      <th>1</th>
      <td>马里奥赛车8</td>
      <td>60</td>
      <td>2017-12-15</td>
    </tr>
    <tr>
      <th>2</th>
      <td>宝可梦·剑</td>
      <td>300</td>
      <td>2019-11-15</td>
    </tr>
    <tr>
      <th>3</th>
      <td>宝可梦·盾</td>
      <td>700</td>
      <td>2019-11-15</td>
    </tr>
    <tr>
      <th>4</th>
      <td>塞尔达传说 旷野之息</td>
      <td>600</td>
      <td>2017-03-03</td>
    </tr>
  </tbody>
</table>
</div>




```python
df1 = pd.read_excel('Desktop/test_data.xlsx',sheet_name=1)
df1
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>游戏名</th>
      <th>游玩时长(h)</th>
      <th>发布时间</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Fate/Grand Order</td>
      <td>900.0</td>
      <td>2015-08-12</td>
    </tr>
    <tr>
      <th>1</th>
      <td>明日方舟</td>
      <td>500.0</td>
      <td>2019-05-01</td>
    </tr>
    <tr>
      <th>2</th>
      <td>世界计划彩色舞台 feat. 初音未来</td>
      <td>100.0</td>
      <td>2020-09-20</td>
    </tr>
    <tr>
      <th>3</th>
      <td>碧蓝航线</td>
      <td>90.0</td>
      <td>2017-06-02</td>
    </tr>
    <tr>
      <th>4</th>
      <td>刀剑神域黑衣剑士：王牌</td>
      <td>NaN</td>
      <td>2021-06-09</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.read_excel('Desktop/test_data.xlsx',sheet_name=None)
```




    {'主机游戏':           游戏名  游玩时长(h)       发布时间
     0  塞尔达传说 旷野之息      600 2017-03-03
     1      马里奥赛车8       60 2017-12-15
     2       宝可梦·剑      300 2019-11-15
     3       宝可梦·盾      700 2019-11-15
     4  塞尔达传说 旷野之息      600 2017-03-03,
     '手机游戏':                    游戏名  游玩时长(h)       发布时间
     0     Fate/Grand Order    900.0 2015-08-12
     1                 明日方舟    500.0 2019-05-01
     2  世界计划彩色舞台 feat. 初音未来    100.0 2020-09-20
     3                 碧蓝航线     90.0 2017-06-02
     4          刀剑神域黑衣剑士：王牌      NaN 2021-06-09}



### **数据处理**  
#### **拼接**  
每一个sheet/文件内的格式是一致时可以用Concat方式将两个文档内的内容合并  
`pd.concat([df1,df2,...],axis=·默认0，0为纵向拼接，1为横向拼接·,ignore_index=·默认False，False为不重置index,纵向拼接时最后重置·)`  


```python
pd.concat([df0,df1],axis=1)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>游戏名</th>
      <th>游玩时长(h)</th>
      <th>发布时间</th>
      <th>游戏名</th>
      <th>游玩时长(h)</th>
      <th>发布时间</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>塞尔达传说 旷野之息</td>
      <td>600</td>
      <td>2017-03-03</td>
      <td>Fate/Grand Order</td>
      <td>900.0</td>
      <td>2015-08-12</td>
    </tr>
    <tr>
      <th>1</th>
      <td>马里奥赛车8</td>
      <td>60</td>
      <td>2017-12-15</td>
      <td>明日方舟</td>
      <td>500.0</td>
      <td>2019-05-01</td>
    </tr>
    <tr>
      <th>2</th>
      <td>宝可梦·剑</td>
      <td>300</td>
      <td>2019-11-15</td>
      <td>世界计划彩色舞台 feat. 初音未来</td>
      <td>100.0</td>
      <td>2020-09-20</td>
    </tr>
    <tr>
      <th>3</th>
      <td>宝可梦·盾</td>
      <td>700</td>
      <td>2019-11-15</td>
      <td>碧蓝航线</td>
      <td>90.0</td>
      <td>2017-06-02</td>
    </tr>
    <tr>
      <th>4</th>
      <td>塞尔达传说 旷野之息</td>
      <td>600</td>
      <td>2017-03-03</td>
      <td>刀剑神域黑衣剑士：王牌</td>
      <td>NaN</td>
      <td>2021-06-09</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.concat([df0,df1])
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>游戏名</th>
      <th>游玩时长(h)</th>
      <th>发布时间</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>塞尔达传说 旷野之息</td>
      <td>600.0</td>
      <td>2017-03-03</td>
    </tr>
    <tr>
      <th>1</th>
      <td>马里奥赛车8</td>
      <td>60.0</td>
      <td>2017-12-15</td>
    </tr>
    <tr>
      <th>2</th>
      <td>宝可梦·剑</td>
      <td>300.0</td>
      <td>2019-11-15</td>
    </tr>
    <tr>
      <th>3</th>
      <td>宝可梦·盾</td>
      <td>700.0</td>
      <td>2019-11-15</td>
    </tr>
    <tr>
      <th>4</th>
      <td>塞尔达传说 旷野之息</td>
      <td>600.0</td>
      <td>2017-03-03</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Fate/Grand Order</td>
      <td>900.0</td>
      <td>2015-08-12</td>
    </tr>
    <tr>
      <th>1</th>
      <td>明日方舟</td>
      <td>500.0</td>
      <td>2019-05-01</td>
    </tr>
    <tr>
      <th>2</th>
      <td>世界计划彩色舞台 feat. 初音未来</td>
      <td>100.0</td>
      <td>2020-09-20</td>
    </tr>
    <tr>
      <th>3</th>
      <td>碧蓝航线</td>
      <td>90.0</td>
      <td>2017-06-02</td>
    </tr>
    <tr>
      <th>4</th>
      <td>刀剑神域黑衣剑士：王牌</td>
      <td>NaN</td>
      <td>2021-06-09</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2 = pd.concat([df0,df1],ignore_index=True)
df2
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>游戏名</th>
      <th>游玩时长(h)</th>
      <th>发布时间</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>塞尔达传说 旷野之息</td>
      <td>600.0</td>
      <td>2017-03-03</td>
    </tr>
    <tr>
      <th>1</th>
      <td>马里奥赛车8</td>
      <td>60.0</td>
      <td>2017-12-15</td>
    </tr>
    <tr>
      <th>2</th>
      <td>宝可梦·剑</td>
      <td>300.0</td>
      <td>2019-11-15</td>
    </tr>
    <tr>
      <th>3</th>
      <td>宝可梦·盾</td>
      <td>700.0</td>
      <td>2019-11-15</td>
    </tr>
    <tr>
      <th>4</th>
      <td>塞尔达传说 旷野之息</td>
      <td>600.0</td>
      <td>2017-03-03</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Fate/Grand Order</td>
      <td>900.0</td>
      <td>2015-08-12</td>
    </tr>
    <tr>
      <th>6</th>
      <td>明日方舟</td>
      <td>500.0</td>
      <td>2019-05-01</td>
    </tr>
    <tr>
      <th>7</th>
      <td>世界计划彩色舞台 feat. 初音未来</td>
      <td>100.0</td>
      <td>2020-09-20</td>
    </tr>
    <tr>
      <th>8</th>
      <td>碧蓝航线</td>
      <td>90.0</td>
      <td>2017-06-02</td>
    </tr>
    <tr>
      <th>9</th>
      <td>刀剑神域黑衣剑士：王牌</td>
      <td>NaN</td>
      <td>2021-06-09</td>
    </tr>
  </tbody>
</table>
</div>



#### 在不知道有多少sheet的同时并增加sheet名


```python
sheet_name_list = list(pd.read_excel('Desktop/test_data.xlsx',sheet_name=None).keys())
df0=[]
for i in sheet_name_list:
    df1 = pd.read_excel('Desktop/test_data.xlsx',sheet_name=i)
    df1['游戏平台'] = i
    df0.append(df1)
df2 = pd.concat(df0,ignore_index=True)
df2
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>游戏名</th>
      <th>游玩时长(h)</th>
      <th>发布时间</th>
      <th>游戏平台</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>塞尔达传说 旷野之息</td>
      <td>600.0</td>
      <td>2017-03-03</td>
      <td>主机游戏</td>
    </tr>
    <tr>
      <th>1</th>
      <td>马里奥赛车8</td>
      <td>60.0</td>
      <td>2017-12-15</td>
      <td>主机游戏</td>
    </tr>
    <tr>
      <th>2</th>
      <td>宝可梦·剑</td>
      <td>300.0</td>
      <td>2019-11-15</td>
      <td>主机游戏</td>
    </tr>
    <tr>
      <th>3</th>
      <td>宝可梦·盾</td>
      <td>700.0</td>
      <td>2019-11-15</td>
      <td>主机游戏</td>
    </tr>
    <tr>
      <th>4</th>
      <td>塞尔达传说 旷野之息</td>
      <td>600.0</td>
      <td>2017-03-03</td>
      <td>主机游戏</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Fate/Grand Order</td>
      <td>900.0</td>
      <td>2015-08-12</td>
      <td>手机游戏</td>
    </tr>
    <tr>
      <th>6</th>
      <td>明日方舟</td>
      <td>500.0</td>
      <td>2019-05-01</td>
      <td>手机游戏</td>
    </tr>
    <tr>
      <th>7</th>
      <td>世界计划彩色舞台 feat. 初音未来</td>
      <td>100.0</td>
      <td>2020-09-20</td>
      <td>手机游戏</td>
    </tr>
    <tr>
      <th>8</th>
      <td>碧蓝航线</td>
      <td>90.0</td>
      <td>2017-06-02</td>
      <td>手机游戏</td>
    </tr>
    <tr>
      <th>9</th>
      <td>刀剑神域黑衣剑士：王牌</td>
      <td>NaN</td>
      <td>2021-06-09</td>
      <td>手机游戏</td>
    </tr>
  </tbody>
</table>
</div>



#### **去重**  
`df.drop_duplicates(subset=·默认None，指全部·, keep={'first'，'last'},inplace=·默认False，指直接覆盖·, ignore_index=False)`


```python
df2.drop_duplicates()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>游戏名</th>
      <th>游玩时长(h)</th>
      <th>发布时间</th>
      <th>游戏平台</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>塞尔达传说 旷野之息</td>
      <td>600.0</td>
      <td>2017-03-03</td>
      <td>主机游戏</td>
    </tr>
    <tr>
      <th>1</th>
      <td>马里奥赛车8</td>
      <td>60.0</td>
      <td>2017-12-15</td>
      <td>主机游戏</td>
    </tr>
    <tr>
      <th>2</th>
      <td>宝可梦·剑</td>
      <td>300.0</td>
      <td>2019-11-15</td>
      <td>主机游戏</td>
    </tr>
    <tr>
      <th>3</th>
      <td>宝可梦·盾</td>
      <td>700.0</td>
      <td>2019-11-15</td>
      <td>主机游戏</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Fate/Grand Order</td>
      <td>900.0</td>
      <td>2015-08-12</td>
      <td>手机游戏</td>
    </tr>
    <tr>
      <th>6</th>
      <td>明日方舟</td>
      <td>500.0</td>
      <td>2019-05-01</td>
      <td>手机游戏</td>
    </tr>
    <tr>
      <th>7</th>
      <td>世界计划彩色舞台 feat. 初音未来</td>
      <td>100.0</td>
      <td>2020-09-20</td>
      <td>手机游戏</td>
    </tr>
    <tr>
      <th>8</th>
      <td>碧蓝航线</td>
      <td>90.0</td>
      <td>2017-06-02</td>
      <td>手机游戏</td>
    </tr>
    <tr>
      <th>9</th>
      <td>刀剑神域黑衣剑士：王牌</td>
      <td>NaN</td>
      <td>2021-06-09</td>
      <td>手机游戏</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2.drop_duplicates(keep='last')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>游戏名</th>
      <th>游玩时长(h)</th>
      <th>发布时间</th>
      <th>游戏平台</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>马里奥赛车8</td>
      <td>60.0</td>
      <td>2017-12-15</td>
      <td>主机游戏</td>
    </tr>
    <tr>
      <th>2</th>
      <td>宝可梦·剑</td>
      <td>300.0</td>
      <td>2019-11-15</td>
      <td>主机游戏</td>
    </tr>
    <tr>
      <th>3</th>
      <td>宝可梦·盾</td>
      <td>700.0</td>
      <td>2019-11-15</td>
      <td>主机游戏</td>
    </tr>
    <tr>
      <th>4</th>
      <td>塞尔达传说 旷野之息</td>
      <td>600.0</td>
      <td>2017-03-03</td>
      <td>主机游戏</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Fate/Grand Order</td>
      <td>900.0</td>
      <td>2015-08-12</td>
      <td>手机游戏</td>
    </tr>
    <tr>
      <th>6</th>
      <td>明日方舟</td>
      <td>500.0</td>
      <td>2019-05-01</td>
      <td>手机游戏</td>
    </tr>
    <tr>
      <th>7</th>
      <td>世界计划彩色舞台 feat. 初音未来</td>
      <td>100.0</td>
      <td>2020-09-20</td>
      <td>手机游戏</td>
    </tr>
    <tr>
      <th>8</th>
      <td>碧蓝航线</td>
      <td>90.0</td>
      <td>2017-06-02</td>
      <td>手机游戏</td>
    </tr>
    <tr>
      <th>9</th>
      <td>刀剑神域黑衣剑士：王牌</td>
      <td>NaN</td>
      <td>2021-06-09</td>
      <td>手机游戏</td>
    </tr>
  </tbody>
</table>
</div>




```python
df3 = df2.drop_duplicates(ignore_index=True)
df3
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>游戏名</th>
      <th>游玩时长(h)</th>
      <th>发布时间</th>
      <th>游戏平台</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>塞尔达传说 旷野之息</td>
      <td>600.0</td>
      <td>2017-03-03</td>
      <td>主机游戏</td>
    </tr>
    <tr>
      <th>1</th>
      <td>马里奥赛车8</td>
      <td>60.0</td>
      <td>2017-12-15</td>
      <td>主机游戏</td>
    </tr>
    <tr>
      <th>2</th>
      <td>宝可梦·剑</td>
      <td>300.0</td>
      <td>2019-11-15</td>
      <td>主机游戏</td>
    </tr>
    <tr>
      <th>3</th>
      <td>宝可梦·盾</td>
      <td>700.0</td>
      <td>2019-11-15</td>
      <td>主机游戏</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Fate/Grand Order</td>
      <td>900.0</td>
      <td>2015-08-12</td>
      <td>手机游戏</td>
    </tr>
    <tr>
      <th>5</th>
      <td>明日方舟</td>
      <td>500.0</td>
      <td>2019-05-01</td>
      <td>手机游戏</td>
    </tr>
    <tr>
      <th>6</th>
      <td>世界计划彩色舞台 feat. 初音未来</td>
      <td>100.0</td>
      <td>2020-09-20</td>
      <td>手机游戏</td>
    </tr>
    <tr>
      <th>7</th>
      <td>碧蓝航线</td>
      <td>90.0</td>
      <td>2017-06-02</td>
      <td>手机游戏</td>
    </tr>
    <tr>
      <th>8</th>
      <td>刀剑神域黑衣剑士：王牌</td>
      <td>NaN</td>
      <td>2021-06-09</td>
      <td>手机游戏</td>
    </tr>
  </tbody>
</table>
</div>



#### **去除空值**  
`df.dropna(axis=0,inplace=False)`


```python
df4 = df3.dropna()
df4
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>游戏名</th>
      <th>游玩时长(h)</th>
      <th>发布时间</th>
      <th>游戏平台</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>塞尔达传说 旷野之息</td>
      <td>600.0</td>
      <td>2017-03-03</td>
      <td>主机游戏</td>
    </tr>
    <tr>
      <th>1</th>
      <td>马里奥赛车8</td>
      <td>60.0</td>
      <td>2017-12-15</td>
      <td>主机游戏</td>
    </tr>
    <tr>
      <th>2</th>
      <td>宝可梦·剑</td>
      <td>300.0</td>
      <td>2019-11-15</td>
      <td>主机游戏</td>
    </tr>
    <tr>
      <th>3</th>
      <td>宝可梦·盾</td>
      <td>700.0</td>
      <td>2019-11-15</td>
      <td>主机游戏</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Fate/Grand Order</td>
      <td>900.0</td>
      <td>2015-08-12</td>
      <td>手机游戏</td>
    </tr>
    <tr>
      <th>5</th>
      <td>明日方舟</td>
      <td>500.0</td>
      <td>2019-05-01</td>
      <td>手机游戏</td>
    </tr>
    <tr>
      <th>6</th>
      <td>世界计划彩色舞台 feat. 初音未来</td>
      <td>100.0</td>
      <td>2020-09-20</td>
      <td>手机游戏</td>
    </tr>
    <tr>
      <th>7</th>
      <td>碧蓝航线</td>
      <td>90.0</td>
      <td>2017-06-02</td>
      <td>手机游戏</td>
    </tr>
  </tbody>
</table>
</div>



#### **空值填充**  
`df.fillna(value=None, method={‘backfill’, ‘bfill’, ‘pad’, ‘ffill’, None})`


```python
df3.fillna('狗都不玩')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>游戏名</th>
      <th>游玩时长(h)</th>
      <th>发布时间</th>
      <th>游戏平台</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>塞尔达传说 旷野之息</td>
      <td>600</td>
      <td>2017-03-03</td>
      <td>主机游戏</td>
    </tr>
    <tr>
      <th>1</th>
      <td>马里奥赛车8</td>
      <td>60</td>
      <td>2017-12-15</td>
      <td>主机游戏</td>
    </tr>
    <tr>
      <th>2</th>
      <td>宝可梦·剑</td>
      <td>300</td>
      <td>2019-11-15</td>
      <td>主机游戏</td>
    </tr>
    <tr>
      <th>3</th>
      <td>宝可梦·盾</td>
      <td>700</td>
      <td>2019-11-15</td>
      <td>主机游戏</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Fate/Grand Order</td>
      <td>900</td>
      <td>2015-08-12</td>
      <td>手机游戏</td>
    </tr>
    <tr>
      <th>5</th>
      <td>明日方舟</td>
      <td>500</td>
      <td>2019-05-01</td>
      <td>手机游戏</td>
    </tr>
    <tr>
      <th>6</th>
      <td>世界计划彩色舞台 feat. 初音未来</td>
      <td>100</td>
      <td>2020-09-20</td>
      <td>手机游戏</td>
    </tr>
    <tr>
      <th>7</th>
      <td>碧蓝航线</td>
      <td>90</td>
      <td>2017-06-02</td>
      <td>手机游戏</td>
    </tr>
    <tr>
      <th>8</th>
      <td>刀剑神域黑衣剑士：王牌</td>
      <td>狗都不玩</td>
      <td>2021-06-09</td>
      <td>手机游戏</td>
    </tr>
  </tbody>
</table>
</div>




```python
df3.fillna(0)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>游戏名</th>
      <th>游玩时长(h)</th>
      <th>发布时间</th>
      <th>游戏平台</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>塞尔达传说 旷野之息</td>
      <td>600.0</td>
      <td>2017-03-03</td>
      <td>主机游戏</td>
    </tr>
    <tr>
      <th>1</th>
      <td>马里奥赛车8</td>
      <td>60.0</td>
      <td>2017-12-15</td>
      <td>主机游戏</td>
    </tr>
    <tr>
      <th>2</th>
      <td>宝可梦·剑</td>
      <td>300.0</td>
      <td>2019-11-15</td>
      <td>主机游戏</td>
    </tr>
    <tr>
      <th>3</th>
      <td>宝可梦·盾</td>
      <td>700.0</td>
      <td>2019-11-15</td>
      <td>主机游戏</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Fate/Grand Order</td>
      <td>900.0</td>
      <td>2015-08-12</td>
      <td>手机游戏</td>
    </tr>
    <tr>
      <th>5</th>
      <td>明日方舟</td>
      <td>500.0</td>
      <td>2019-05-01</td>
      <td>手机游戏</td>
    </tr>
    <tr>
      <th>6</th>
      <td>世界计划彩色舞台 feat. 初音未来</td>
      <td>100.0</td>
      <td>2020-09-20</td>
      <td>手机游戏</td>
    </tr>
    <tr>
      <th>7</th>
      <td>碧蓝航线</td>
      <td>90.0</td>
      <td>2017-06-02</td>
      <td>手机游戏</td>
    </tr>
    <tr>
      <th>8</th>
      <td>刀剑神域黑衣剑士：王牌</td>
      <td>0.0</td>
      <td>2021-06-09</td>
      <td>手机游戏</td>
    </tr>
  </tbody>
</table>
</div>



#### **空值合计**  
`df.isnull().sum()`


```python
df3.isnull().sum()
```




    游戏名        0
    游玩时长(h)    1
    发布时间       0
    游戏平台       0
    dtype: int64



#### lambda处理
`df.apply(lambda x: fun(),axis={0,1})`


```python
df4['Month'] = df4['发布时间'].apply(lambda x: str(x.month)+'月')
df4
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>游戏名</th>
      <th>游玩时长(h)</th>
      <th>发布时间</th>
      <th>游戏平台</th>
      <th>Month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>塞尔达传说 旷野之息</td>
      <td>600.0</td>
      <td>2017-03-03</td>
      <td>主机游戏</td>
      <td>3月</td>
    </tr>
    <tr>
      <th>1</th>
      <td>马里奥赛车8</td>
      <td>60.0</td>
      <td>2017-12-15</td>
      <td>主机游戏</td>
      <td>12月</td>
    </tr>
    <tr>
      <th>2</th>
      <td>宝可梦·剑</td>
      <td>300.0</td>
      <td>2019-11-15</td>
      <td>主机游戏</td>
      <td>11月</td>
    </tr>
    <tr>
      <th>3</th>
      <td>宝可梦·盾</td>
      <td>700.0</td>
      <td>2019-11-15</td>
      <td>主机游戏</td>
      <td>11月</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Fate/Grand Order</td>
      <td>900.0</td>
      <td>2015-08-12</td>
      <td>手机游戏</td>
      <td>8月</td>
    </tr>
    <tr>
      <th>5</th>
      <td>明日方舟</td>
      <td>500.0</td>
      <td>2019-05-01</td>
      <td>手机游戏</td>
      <td>5月</td>
    </tr>
    <tr>
      <th>6</th>
      <td>世界计划彩色舞台 feat. 初音未来</td>
      <td>100.0</td>
      <td>2020-09-20</td>
      <td>手机游戏</td>
      <td>9月</td>
    </tr>
    <tr>
      <th>7</th>
      <td>碧蓝航线</td>
      <td>90.0</td>
      <td>2017-06-02</td>
      <td>手机游戏</td>
      <td>6月</td>
    </tr>
  </tbody>
</table>
</div>




```python
def get_year_month(x):
    y = str(x['发布时间'].year) + '年' + str(x['发布时间'].month) + '月'
    return y
```


```python
df4['年月'] = df4.apply(lambda x : get_year_month(x),axis=1)
df4
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>游戏名</th>
      <th>游玩时长(h)</th>
      <th>发布时间</th>
      <th>游戏平台</th>
      <th>Month</th>
      <th>年月</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>塞尔达传说 旷野之息</td>
      <td>600.0</td>
      <td>2017-03-03</td>
      <td>主机游戏</td>
      <td>3月</td>
      <td>2017年3月</td>
    </tr>
    <tr>
      <th>1</th>
      <td>马里奥赛车8</td>
      <td>60.0</td>
      <td>2017-12-15</td>
      <td>主机游戏</td>
      <td>12月</td>
      <td>2017年12月</td>
    </tr>
    <tr>
      <th>2</th>
      <td>宝可梦·剑</td>
      <td>300.0</td>
      <td>2019-11-15</td>
      <td>主机游戏</td>
      <td>11月</td>
      <td>2019年11月</td>
    </tr>
    <tr>
      <th>3</th>
      <td>宝可梦·盾</td>
      <td>700.0</td>
      <td>2019-11-15</td>
      <td>主机游戏</td>
      <td>11月</td>
      <td>2019年11月</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Fate/Grand Order</td>
      <td>900.0</td>
      <td>2015-08-12</td>
      <td>手机游戏</td>
      <td>8月</td>
      <td>2015年8月</td>
    </tr>
    <tr>
      <th>5</th>
      <td>明日方舟</td>
      <td>500.0</td>
      <td>2019-05-01</td>
      <td>手机游戏</td>
      <td>5月</td>
      <td>2019年5月</td>
    </tr>
    <tr>
      <th>6</th>
      <td>世界计划彩色舞台 feat. 初音未来</td>
      <td>100.0</td>
      <td>2020-09-20</td>
      <td>手机游戏</td>
      <td>9月</td>
      <td>2020年9月</td>
    </tr>
    <tr>
      <th>7</th>
      <td>碧蓝航线</td>
      <td>90.0</td>
      <td>2017-06-02</td>
      <td>手机游戏</td>
      <td>6月</td>
      <td>2017年6月</td>
    </tr>
  </tbody>
</table>
</div>



### 数据统计  
#### 最大值、最小值、平均值
`df.max()
df.min()
df.mean()`


```python
df4['游玩时长(h)'].max()
```




    900.0




```python
df4['游玩时长(h)'].min()
```




    60.0




```python
df4['游玩时长(h)'].mean()
```




    406.25



##### 主机游戏的平均游玩时长


```python
df4[df4['游戏平台'] == '主机游戏']['游玩时长(h)'].mean()
```




    415.0



##### 手机游戏游玩时长最长的游戏


```python
df4[df4['游玩时长(h)'] == df4['游玩时长(h)'].max()]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>游戏名</th>
      <th>游玩时长(h)</th>
      <th>发布时间</th>
      <th>游戏平台</th>
      <th>Month</th>
      <th>年月</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>Fate/Grand Order</td>
      <td>900.0</td>
      <td>2015-08-12</td>
      <td>手机游戏</td>
      <td>8月</td>
      <td>2015年8月</td>
    </tr>
  </tbody>
</table>
</div>



# 未完待续！


```python

```
