#Python-Set
##简介
* set是一个无序的集合
* set中可以存放各种类型的数据
* set具有元素唯一性，无重复元素
* set()可以创建一个空的set
##操作符
![](http://simplebrightman.github.io/blog/images/python/4.JPG)
##函数
![](http://simplebrightman.github.io/blog/images/python/5.JPG)

	In [1]: myset = {False,4.5,3,6,'cat'}
	
	In [2]: yourset = {99,3,100}
	
	In [3]:
	In [3]: myset.union(yourset)
	Out[3]: {False, 3, 4.5, 6, 99, 100, 'cat'}
	
	In [4]: myset | yourset
	Out[4]: {False, 3, 4.5, 6, 99, 100, 'cat'}
	
	In [5]: myset.intersection(yourset)
	Out[5]: {3}
	
	In [6]: myset&yourset
	Out[6]: {3}
	
	In [7]: myset.diff
	myset.difference        myset.difference_update
	
	In [7]: myset.difference(yourset)
	Out[7]: {False, 4.5, 6, 'cat'}
	
	In [8]: myset - yourset
	Out[8]: {False, 4.5, 6, 'cat'}
	
	In [9]: {3,100}.issubset(yourset)
	Out[9]: True
	
	In [10]: {3,100}<=yourset
	Out[10]: True
	
	In [11]: myset.add("house")
	
	In [12]: myset
	Out[12]: {False, 3, 4.5, 6, 'cat', 'house'}
	
	In [13]: myset.clear()
	
	In [14]: myset
	Out[14]: set()