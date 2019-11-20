# 链表

## 缓存淘汰策略
* 先进先出策略 FIFO （ First In ， First Out ）
* 最少使用策略 LFU （ Least Frequently Used ）
* 最近最少使用策略 LRU （ Least Recently Used ）

### 如何实现LRU策略
维护一个有序单链表，越靠近链表尾部的结点是越早之前访问的。当有一个新的数据被访问时，我们从链表头开始顺序遍历链表。
1. 如果此数据之前已经被缓存在链表中了，我们遍历得到这个数据对应的结点，并将其从原来的位置删除，然后再插入到链表的头部。
2. 如果此数据没有在缓存链表中，又可以分为两种情况：
    如果此时缓存未满，则将此结点直接插入到链表的头部； 
    如果此时缓存已满，则链表尾结点删除，将新的数据结点插入链表的头部。

## 概念
* 数组：使用连续的内存空间存储数据；
* 链表：通过“指针”将非连续的内存块串联起来；
    * 结点：内存块 == 数据 + 指针

## 复杂度分析
* 插入、删除 == O(1)；
* 查询 -- O(n) 需要遍历数组；

## 循环链表
* 适合处理环形数据结构 -- 约瑟夫斯问题


### 约瑟夫斯问题

``` yaml
if n = 2^a + l where l < 2a
w(n) = 2l +1

---
41 = 2^5 + 2^3 + 2^0
   = 10101 ==> 01011 ==> 2^0 + 2^1 + 2^4 = 19
```

``` python
# -*- coding: utf-8 -*- 
class Node(object):
	def __init__(self, value):
		self.value = value 
		self.next = None

def create_linkList(n):
	head = Node(1)
	pre = head
	for i in range(2, n+1):
		newNode = Node(i)
		pre.next= newNode
		pre = newNode
	pre.next = head
	return head

n = 5 #总的个数
m = 2 #数的数目
if m == 1: #如果是1的话，特殊处理，直接输出
	print (n)  
else:
	head = create_linkList(n)
	pre = None
	cur = head
	while cur.next != cur: #终止条件是节点的下一个节点指向本身
		for i in range(m-1):
			pre =  cur
			cur = cur.next
		print (cur.value)
		pre.next = cur.next
		cur.next = None
		cur = pre.next
	print (cur.value)
```

## 双向链表
* 每个节点同时存在`前驱指针`、`后继指针`；
* 更多的内存空间；
* 插入、删除比单向链表更加高效；
    * 删除：删除结点中数据等于给定值 && 删除指定指针的结点O(1)
* 有序链表，按值查询更加高效；

## 双向循环链表


## 程序是用来干什么的？
记得上大学时，参加算法竞赛，认为规律是最重要的，去猜测问题规律，得出正确结论；经常会出现错误，当时问题，如果规律 >> 程序计算结果；

但是，程序就是用来验证结果的，在充分证明规则是正确之前，将问题程序化，得到结果，是最准确的；当然，替换为规律更加高效；