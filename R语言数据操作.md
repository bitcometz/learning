# 目录
* [背景介绍](#背景介绍)
* [R中的数据](#R中的数据)
   * [模式和类](#模式和类)
   * [R的数据存储](#R的数据存储)
   * [R对象的结构](#R对象的结构)
   * [对象的转换](#对象的转换)
   * [缺省值](#缺省值)


## 背景介绍
R语言调用函数都是非常方便，痛点往往在于如何把数据整理成函数需要点格式，包括：增、减、改等多种操作。本网页等内容来之《R语言数据操作》。

## R中的数据
R语言的对象（Objects）主要包括向量、矩阵、数组、数据框和列表。

![image](https://github.com/bitcometz/images/blob/master/R_duixiang.png)

### 模式和类

R中每一个对象包含多个属性来描述该对象中的信息的性质，其中最重要的两个属性是模式和类。其中`mode函数`表示对象的模式，`class函数`表示对象的类。
当需要查看列表各个组成部分当模式当时候，可以采取`sapply函数`：
```
> mylist = list(a=c(1,2,3), b=c("cat","dog","duck"), d=factor("a","b","c"))
> sapply(mylist, class)
          a           b           d 
  "numeric" "character"    "factor" 
> sapply(mylist, mode)
          a           b           d 
  "numeric" "character"   "numeric"
```
此外，R还提供了`typeof函数`，或者以`is.`开头的函数，来检测一个对象是否属于某一特定类型，例如`is.list, is.factor, is.numeric, is.data.fam, is.character`

### R的数据存储
单个数值的存储在R里面是非常少用的，用的最多是用`c函数`来保存数据集合，combine. 注意`c函数`可以合并数值和向量，如果合并不同模式的时候，不同的模式最后会变成一样。
```
> x=c(1,2,5,8)
> x
[1] 1 2 5 8
> mode(x)
[1] "numeric"
> y = c(1,2,"cat",3)
> y
[1] "1"   "2"   "cat" "3"  
> mode(y)
[1] "character"
> all = c(x,y)
> all
[1] "1"   "2"   "5"   "8"   "1"   "2"   "cat" "3"  
```
关于R中的**向量**有一个令人惊讶的事实，如果运算涉及两个不同长度的向量，R将对较短对向量进行循环，从而使长度可比。
```
> nums = 1:10
> nums
 [1]  1  2  3  4  5  6  7  8  9 10
> nums + 1
 [1]  2  3  4  5  6  7  8  9 10 11
> nums + c(-5,1)
 [1] -4  3 -2  5  0  7  2  9  4 11
```
**数组**是向量对一个多维延伸，数组中对对象必须是同一个模式，常用对数组为矩阵，nrow和ncol分别表示矩阵对行和列，由于矩阵是按列存储的，所以matrix是假定输入向量是被按列转为矩阵，如果需要按行存储，则可以用`byrow=TRUE`来设置。此外，可以用**dimnames**来指定名称。
```
rmat = matrix(c(1:15),nrow=5,ncol=3,dimnames=list(c('L1','L2','L3','L4','L5'), c('A','B','C')))
> rmat
   A  B  C
L1 1  6 11
L2 2  7 12
L3 3  8 13
L4 4  9 14
L5 5 10 15
```
**列表**提供了单个R对象中存储不同模式的对象：
```
> mylist = list(c(1,4,6), "dog", 'cat', "TRUE", c(9,10,11))
> mylist
[[1]]
[1] 1 4 6

[[2]]
[1] "dog"

[[3]]
[1] "cat"

[[4]]
[1] "TRUE"

[[5]]
[1]  9 10 11

> sapply(mylist, mode)
[1] "numeric"   "character" "character" "character" "numeric" 
```
**数据框**也是一个列表，限制条件是列表中每一个元素的长度必须**相同**。

### R对象的结构
某些情况下，直接打印给出太多细节，然后**summary**或者类似函数提供太少的细节，`str函数`可提供一个可行的妥协方案
```
> nestlist = list(
+ a = list(matrix(rnorm(10),5,2),val=3),
+ b = list(sample(letters,10),values=runif(5)),
+ c = list(list(1:10, 1:20),list(1:5,1:10)))
> summary(nestlist)
  Length Class  Mode
a 2      -none- list
b 2      -none- list
c 2      -none- list
> str(nestlist)
List of 3
 $ a:List of 2
  ..$    : num [1:5, 1:2] -2.6233 0.0899 1.5775 -0.1641 0.8837 ...
  ..$ val: num 3
 $ b:List of 2
  ..$       : chr [1:10] "j" "h" "o" "u" ...
  ..$ values: num [1:5] 0.8694 0.6104 0.0697 0.4813 0.3236
 $ c:List of 2
  ..$ :List of 2
  .. ..$ : int [1:10] 1 2 3 4 5 6 7 8 9 10
  .. ..$ : int [1:20] 1 2 3 4 5 6 7 8 9 10 ...
  ..$ :List of 2
  .. ..$ : int [1:5] 1 2 3 4 5
  .. ..$ : int [1:10] 1 2 3 4 5 6 7 8 9 10
```
### 对象的转换
R提供了多种**暂时**改变对象行为的常规转换方式，每一种都以".as"开头。
```
> nums = c(12,10,8,12,10,8,10,12,8)
> tt = table(nums)
> tt
nums
 8 10 12 
 3  3  3 
> names(tt)
[1] "8"  "10" "12"
> sum(nums)
[1] 90
> sum(as.numeric(names(tt))*tt)
[1] 90
```
### 缺省值









