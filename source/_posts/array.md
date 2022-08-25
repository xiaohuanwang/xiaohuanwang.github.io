---
title: 数据结构-数组Array
date: 2019-10-22 15:29:34
index_img: http://image.wangxiaohuan.com/blog/image/202208251029181.png
banner_img: http://image.wangxiaohuan.com/blog/image/202208251029181.png
categories:
- 数据结构
tags:
- 数组
---

数组时一种最常用的数据结构，下标索引从0开始。

### 数组的定义和特点

  数组：数组（Array）是一种线性表数据结构。用一组连续的内存空间，储存一组具有相同类型的数据。

*   线性表，线性表就是数据排成一条线一样的数据结构。上面的数据最多只有前和后两个方向。
*   连续的内存空间和相同类型的数据。

### 数组的优点和缺点

##### 优点

* 数组支持随机访问，根据下标随机访问的时间复杂度为O(1)。
* 构建非常简单。 int[] array=new int[5]；

##### 缺点
* 查询某个元素是否存在时，需要遍历整个数据，删除和增加某个元素时，其时间复杂度为O(n)。
* 构建数组时，必须分配一段连续的内存空间。

### 创建并初始化数组代码实现

在java程序中，创建一个数组需要三步：

1. 声明数组的名字和类型。
2. 创建数组。
3. 初始化数组元素。

```
//完整模式
int[] a;   //声明数组的名字和类型
a=new int[10];  //创建数组
for(int i=0;i<10;i++){
  a[i]=i;   //初始化数组
}
//简化模式创建数组
int[] a=new int[4];
int[] a={1,2,3,4};
```
找出数组中最大的元素
```
public class MaxArray {

	public static void main(String[] args) {
		int[] a = {1,3,2,5,6,7,4,8};
		int max=a[0];
		for(int i=0;i<a.length;i++) {
			if(a[i]>max) {
				max=a[i];
			}
		}
		System.out.println(max);

	}
}
```
计算数组元素的平均值

```
public class AverageArray {

	public static void main(String[] args) {
		int[] a = {1,2,3,4,5,6,7,8};
		int n = a.length;
		double sum=0.0;
		for(int i=0;i<n;i++) {
			sum=sum+a[i];
		}
		double average=sum/n;
		System.out.println(average);
	}

}
```
复制数组

```
public class CopyArray {
    public static void main(String[] args){
        int[] a = {1,2,3,4,5,6};
        int n = a.length;
        int[] b = new int[n];
        for (int i=0;i<n;i++){
            b[i] = a[i];
        }
        System.out.print(b.length);
    }
}
```

翻转数组

```
public class FlipArray {
    public static void main(String[] args){
        int[] a = {1,2,3,4,5,6};
        int n=a.length;
        for (int i=0;i<n/2;i++){
            int temp=a[i];
            a[i]=a[n-i-1];
            a[n-i-1]=temp;
        }
        System.out.print(a);
    }
}
```

* 实现一个支持动态扩容的数组。
* 实现一个大小固定的有序数组，支持动态增删改操作。
* 实现两个有序的数组合并成一个有序数组。
