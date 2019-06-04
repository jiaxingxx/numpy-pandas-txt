1. 如果想仅进行简单的“拼接”而不是合并呢，要使用concat函数：

df = pd.concat( [df_user, dummies_sex, dummies_age, dummies_level], axis=1 )

这样可以保留这些表单的全部信息，参数axis=1表示列拼接，axis=0表示行拼接。

要保证背个表单的行数是相同的，并且每一行对应的key也是相同的，列拼接才变得有意义

详细:(https://blog.csdn.net/zzpdbk/article/details/79232661)
