# numpy 用法记录
  
  
## 1.频率和众数
可用scipy.stats模块提供的mode函数，求出数组中最高频率值
```
from scipy.stats import mode
list1 = [1, 2, 3, 4, 1, 3]
print(mode(list1))

output:
ModeResult(mode=array([1]), count=array([2]))
```
由此可见，其亦支持numpy的array，因此也可用array求众数，对一维array我们可得出
```
print("list1中最常见的成员为：{}，出现了{}次。".format(mode(list1)[0][0], mode(list1)[1][0]))

output:
list1中最常见的成员为：1，出现了2次。
```
对于二维array，可有如下:
```
arr = np.array([[1, 1, 3],[2, 2, 3], [1, 3, 3]])
print(mode(arr))

output:
ModeResult(mode=array([[1, 1, 3]]), count=array([[2, 1, 3]]))
```
可见它将每一行的众数（mode）输出，并以array形式返回，我们只需用
```
print("# arr的每一列中最常见的成员为：{}，分别出现了{}次。".format(mode(arr)[0][0], mode(arr)[1][0]))
print("# arr的第一列中最常见的成员为：{}，出现了{}次。".format(mode(arr)[0][0][0], mode(arr)[1][0][0]))
print("# arr的每一行中最常见的成员为：{}，分别出现了{}次。".format(mode(arr.transpose())[0][0], mode(arr.transpose())[1][0]))
print("# arr中最常见的成员为：{}，出现了{}次。".format(mode(arr.reshape(-1))[0][0], mode(arr.reshape(-1))[1][0]))

output:
# arr的每一列中最常见的成员为：[1 1 3]，分别出现了[2 1 3]次。
# arr的第一列中最常见的成员为：1，出现了2次。
# arr的每一行中最常见的成员为：[1 2 3]，分别出现了[2 2 2]次。
# arr中最常见的成员为：3，出现了4次。
```
  
## 2.均值与中位数
```
print("list1均值为：", np.mean(list1))
print("list1中位数为：", np.median(list1))

output：
list1均值为： 2.3333333333333335
list1中位数为： 2.5
```
## 3.极差与方差
```
print("list1极差为：", np.ptp(list1))
print("list1方差为", np.var(list1))
print("list1标准差为：", np.std(list1))

output:
list1极差为： 3
list1方差为 1.2222222222222223
list1标准差为： 1.1055415967851334
```
## 4.百分位数（percentile）与箱线图（box plot）
百分位数指的是数据从小到大排序后，计算相应的累计百分位，则某一个百分位所对应数据的值为该百分位的百分位数，我们可以从高中学到的从频率图中找中位数处得到灵感,p%位置对应的第p百分位数。下例子中，显然第100百分位数为4.
```
print("list10%处的百分位数为：", np.percentile(list1, 0))

output:
list1位置0处的百分位数为： 1.0
```
有了百分位数后，我们可以得出箱型图的定义，用数据的5个百分位特征值:第10个百分位，第25个百分位，第50个百分位，第75个百分位,第90个百分位来描述数据的图形,离群值用“+”表示。
我们用matplotlib辅助之。
箱型图的具体绘制可见[经典数据集](经典数据集.md)鸢尾花部分。

