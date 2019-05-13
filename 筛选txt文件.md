1.从记录中选出所有fault_code列的值在fault_list= [487, 479, 500, 505]这个范围内的记录
要筛选的值一定是储存在list中，在dataframe中会返回空值
例如：
record2=record[record['FAULT_CODE'].isin(fault_list)]

2.merge
result = pd.merge(left, right, how='inner', on=['key1', 'key2'])
![image](https://github.com/jiaxingxx/numpy-pandas-txt/blob/master/merging_merge_on_key_inner.png)

3.pd.merge()方法设置连接方法。
主要包括inner（内连接）、outer（外链接）、left（左连接）、right（右连接）。
参数how默认值是inner内连接，上面的都是采用内连接，连接两边都有的值。
当采用outer外连接时，会取并集，并用NaN填充。
外连接其实左连接和右连接的并集。左连接是左侧DataFrame取全部数据，右侧DataFrame匹配左侧DataFrame。（右连接right和左连接类似）

4.import pandas as pd

# 删除含有空数据的全部行

df4 = pd.read_csv('4.csv',  encoding='utf-8')

df4 = df4.dropna()

# 可以通过axis参数来删除含有空数据的全部列

df4 = df4.dropna(axis=1)

# 可以通过subset参数来删除在age和sex中含有空数据的全部行

df4 = df4.dropna(subset=["age", "sex"])

print(df4)

df4 = df4.dropna(subset=['age', 'body','home.dest'])

5.对pandas重置index从0到n
df = df.reset_index(drop=True)

6.在做文本分析的时候，修改一个DataFrame的column名称，总结如下： 
数据如下：

方法一：暴力方法
>>>a.columns = ['a','b','c']
>>>a
   a  b  c
0  1  4  7
1  2  5  8
2  3  6  9
但是缺点是必须写三个，要不报错。

方法二：较好的方法
>>>a.rename(columns={'A':'a', 'B':'b', 'C':'c'}, inplace = True)

