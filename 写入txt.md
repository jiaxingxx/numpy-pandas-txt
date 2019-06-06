1.pandas to_csv() 是可以向已经存在的具有相同结构的csv文件增加dataframe数据。

df.to_csv('my_csv.csv', mode='a', header=False)

to_csv()方法mode默认为w，我们加上mode='a'，便可以追加写入数据。


2.python保存numpy数据：

numpy.savetxt("result.txt", numpy_data)
