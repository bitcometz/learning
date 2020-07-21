# 目录
* [背景介绍](#背景介绍)


## 背景介绍
R语言调用函数都是非常方便，痛点往往在于如何把数据整理成函数需要点格式，包括：增、减、改等多种操作。本网页等内容来之《R语言数据操作》。

## R中的数据
R语言的对象（Objects）主要包括向量、矩阵、数组、数据框和列表。

![image](https://github.com/bitcometz/images/blob/master/R_duixiang.png)

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




