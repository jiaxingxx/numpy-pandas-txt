1.从记录中选出所有fault_code列的值在fault_list= [487, 479, 500, 505]这个范围内的记录
要筛选的值一定是储存在list中，在dataframe中会返回空值
例如：
record2=record[record['FAULT_CODE'].isin(fault_list)]

2.merge
result = pd.merge(left, right, how='inner', on=['key1', 'key2'])
![image]https://github.com/jiaxingxx/numpy-pandas-txt/blob/master/merging_merge_on_key_inner.png


