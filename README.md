#Test 01
sum = 2
number = 2
while number <= 100:
       sum = sum + number
       number = number + 2
print(sum)

#Test 02
from pandas import Series, DataFrame
data = {'张飞': [68, 65, 30], '关羽': [95, 76, 98], '刘备': [98, 86, 88], '典韦': [90, 88, 77], '许褚': [80, 90, 90]}
df = DataFrame(data, index=['语文', '数学', '英语'], columns=['张飞', '关羽', '刘备', '典韦', '许褚'])
print(df.mean())#平均值
print(df.min())#最小值
print(df.max())#最大值
print(df.var())#方差
print(df.std())#标准差
#总成绩及排序
data_sum=df1.sum(axis=0)
print(data_sum.sort_values(ascending=False))


#Test 03
# 对汽车投诉信息进行分析
import pandas as pd
#读取数据，把数据链接地址填写在下面
result= pd.read_csv('E:\Python/Data_Engine_with_Python-master/Data_Engine_with_Python-master/L1/car_data_analyze/car_complain.csv')
#print(result)，将genres进行one-hot编码（离散特征有多少取值，就用多少维来表示这个特征）
#数据拆分
result = result.drop(columns='problem').join(result['problem'].str.get_dummies(','))
tags = result.columns[7:]
#品牌投诉总数
print("     品牌投诉总数     ")
df=result.groupby(['brand'])['id'].agg(['count']).sort_values('count',ascending=False)
print(df)
#车型投诉总数
print("     车型投诉总数     ")
df1=result.groupby(['car_model'])['id'].agg(['count']).sort_values('count',ascending=False)
print(df1)
#各品牌平均车型投诉数量
print("     各品牌平均车型投诉数量     ")
df2=result.groupby(['brand','car_model'])['id'].agg(['count']).groupby(['brand']).agg('mean')
df2=df2.sort_values('count',ascending=False)
print(df2)
