#python-tuple
##简介
* tuple是一个有序的集合
* tuple和list很类似，但是tuple中元素不可更改
##tuple操作
	In [1]: myTuple = (2,True,4,96)
	
	In [2]: myTuple
	Out[2]: (2, True, 4, 96)
	
	In [3]: len(myTuple)
	Out[3]: 4
	
	In [4]: myTuple*3
	Out[4]: (2, True, 4, 96, 2, True, 4, 96, 2, True, 4, 96)
	
	In [5]: myTuple[0:2]
	Out[5]: (2, True)
	
	In [6]: myTuple[1] = False
	---------------------------------------------------------------------------
	TypeError                                 Traceback (most recent call last)
	<ipython-input-6-eb935a311b80> in <module>()
	----> 1 myTuple[1] = False
	
	TypeError: 'tuple' object does not support item assignment