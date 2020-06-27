pandas学习笔记
---

## 1.1 常用函数
t.index()

t.columns()

t.values()

t.dtypes()

t.ndim()
<img src="https://github.com/MemorialCheng/EverybodyEveryday/blob/master/数据科学/images/pandas01.png" width = "500">

通过标签获取数据
t.loc(["A":"C"],["name","mobile"])

通过位置获取数据
t.iloc([1:3],[2,4])

## 1.2 pandas之字符串方法

t.dropna(axis=0,how="any",inplace=True)

填充NaN空值为0
t.fillna(0)

替换NaN空值为平均值
t.fillna(t.mean())

替换"age"列为空NaN值为平均值，并保存至t["age"]列
t["age"] = t["age"].fillna(t["age"].mean())



