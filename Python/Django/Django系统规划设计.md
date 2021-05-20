[TOC]

# Django的系统设计

## 根据需求设计用例图



## 根据用例图设计类图

每个实体类就是一个模型（mode），需要考虑每个类之间的关系。

![img](Django%E7%B3%BB%E7%BB%9F%E8%A7%84%E5%88%92%E8%AE%BE%E8%AE%A1.assets/basic-class-diagram.png)

将类之间的关系，和每个类内部的属性方法确定后，可以得到较为丰富的类图。

![models](Django%E7%B3%BB%E7%BB%9F%E8%A7%84%E5%88%92%E8%AE%BE%E8%AE%A1.assets/class-diagram.png)

## 线框图



# 系统设计部分总结

深入学习可以参考设计模式，书籍推荐如下：
《大话设计模式》
《Head first 设计模式》
《设计模式》GOF

# 模型设计

模型mode其实就代表了数据库，而模型的编程表现就是“类（class）”

需要在