1.从记录中选出所有fault_code列的值在fault_list= [487, 479, 500, 505]这个范围内的记录

要筛选的值一定是储存在list中，在dataframe中会返回空值

例如：

record2=record[record['FAULT_CODE'].isin(fault_list)]

当然，有时候我们需要去掉不止一个值，这个时候只需要在isin([]）的列表中添加。
更具体来说，例如，对于appID这个属性，我们想去掉appID=278和appID=382的样本。
df[(True-df['appID'].isin([278,382]))]

单列数据筛选并排序
我们使用.loc对lc数据表中grade列为B值的数据条目进行了筛选操作，具体的代码和筛选结果如下。
在代码中lc.loc[]是.loc函数的语法，lc[“grade”] == “B”是具体的筛选条件。由于数据表较大，
因此在最后使用了head()函数只显示前5行筛选结果。从筛选结果来看grade列的值都为B。

lc.loc[lc["grade"] == "B"]


2.merge
result = pd.merge(left, right, how='inner', on=['key1', 'key2'])
![image](https://github.com/jiaxingxx/numpy-pandas-txt/blob/master/merging_merge_on_key_inner.png)

merge 的时候保留原来的index

result=left.reset_index().merge(right,left_on='A',right_on='C').set_index('index')


3.pd.merge()方法设置连接方法。
主要包括inner（内连接）、outer（外链接）、left（左连接）、right（右连接）。
参数how默认值是inner内连接，上面的都是采用内连接，连接两边都有的值。on选择两个共有的列，列名相同
当采用outer外连接时，会取并集，并用NaN填充。
外连接其实左连接和右连接的并集。左连接是左侧DataFrame取全部数据，右侧DataFrame匹配左侧DataFrame。（右连接right和左连接类似）
**merge时要求数据类型相同，可以A=pd.Dataframe(A,dtype=np.float)进行统一
**设置
 a.merge(b, how="left").set_index(a.index)

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

7. 去除重复行方法
DataFrame.drop_duplicates(subset=None, keep='first', inplace=False)

参数
这个drop_duplicate方法是对DataFrame格式的数据，去除特定列下面的重复行。返回DataFrame格式的数据。

subset : column label or sequence of labels, optional 
用来指定特定的列，默认所有列
keep : {‘first’, ‘last’, False}, default ‘first’ 
删除重复项并保留第一次出现的项
inplace : boolean, default False 
是直接在原来数据上修改还是保留一个副本，默认保留副本



8.# 实例2.3：要连接多个键，传递的DataFrame必须具有MultiIndex：
 
left = pd.DataFrame({'key1': ['K0', 'K0', 'K1', 'K2'], 'key2': ['K0', 'K1', 'K0', 'K1'],
                                  'A': ['A0', 'A1', 'A2', 'A3'],'B': ['B0', 'B1', 'B2', 'B3']})
index = pd.MultiIndex.from_tuples([('K0', 'K0'), ('K1', 'K0'), ('K2', 'K0'), ('K2', 'K1')])
right = pd.DataFrame({'C': ['C0', 'C1', 'C2', 'C3'], 'D': ['D0', 'D1', 'D2', 'D3']}, index=index)
    
result = left.join(right, on=['key1', 'key2'])#等价下面
result = pd.merge(left, right, left_on=['key1','key2'], right_index=True,how='left', sort=False)
    
# left                   right                     result
  key1 key2   A   B              C   D          A   B key1 key2    C   D
0   K0   K0  A0  B0      K0 K0  C0  D0      0  A0  B0   K0   K0   C0   D0
1   K0   K1  A1  B1      K1 K0  C1  D1      1  A1  B1   K0   K1  NaN   NaN
2   K1   K0  A2  B2      K2 K0  C2  D2      2  A2  B2   K1   K0   C1   D1
3   K2   K1  A3  B3         K1  C3  D3      3  A3  B3   K2   K1   C3   D3
    
result = left.join(right, on=['key1', 'key2'], how='inner')#等价下面
result = pd.merge(left, right, left_on=['key1','key2'],right_index=True,how='inner', sort=False)
    
# left                   right              result
  key1 key2   A   B              C   D         A   B key1 key2   C   D
0   K0   K0  A0  B0      K0 K0  C0  D0      0  A0  B0   K0   K0  C0  D0
1   K0   K1  A1  B1      K1 K0  C1  D1      2  A2  B2   K1   K0  C1  D1
2   K1   K0  A2  B2      K2 K0  C2  D2      3  A3  B3   K2   K1  C3  D3
3   K2   K1  A3  B3         K1  C3  D3



9. 删除drop用法

labels参数

DataFrame.drop()中的参数labels是要删除的行或者列的名字，删除行还是列由参数axis控制，axis默认为0即按行删除，要想删除列只需令axis=1。

df.drop(['V'],axis=1)

index参数

对于参数index，这个参数只能传入行的名字即它是专为按行删除设置的，axis的值不影响index，axis的值只在给labels传入参数时起作用。

df.drop(index = 'a',axis = 1)
