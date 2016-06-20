#python-Dictionary
##简介
* 字典是一个无序的集合
* 字典有key-value键值对组成
* 字典中的键不可以重复，key的集合可以看成一个set
##操作符
![](http://simplebrightman.github.io/blog/images/python/6.JPG)
##函数
![](http://simplebrightman.github.io/blog/images/python/7.JPG)

	In [15]: d = {"name":"xiaoming","pwd":"123456"}
	
	In [16]: del d["name"]
	
	In [17]: d
	Out[17]: {'pwd': '123456'}
	
	In [18]: d["name"] = "xiaoming"
	
	In [19]: d
	Out[19]: {'name': 'xiaoming', 'pwd': '123456'}
	
	In [20]: keys = d.keys()
	
	In [21]: keys
	Out[21]: ['pwd', 'name']
	
	In [22]: type(keys)
	Out[22]: list
	
	In [23]: d.values()
	Out[23]: ['123456', 'xiaoming']
	
	In [24]: type(d.values())
	Out[24]: list
	
	In [25]: d.items()
	Out[25]: [('pwd', '123456'), ('name', 'xiaoming')]
	
	In [26]: d["test"]
	---------------------------------------------------------------------------
	KeyError                                  Traceback (most recent call last)
	<ipython-input-26-b3c970f9eb2a> in <module>()
	----> 1 d["test"]
	
	KeyError: 'test'
	
	In [27]: d.get("test")	
	
	In [29]: if d.get("test") == None:
	   ....:     print "No this Key"
	   ....:
	No this Key
	
	In [30]: d.get("test","No this key")
	Out[30]: 'No this key'

可见:

* d.keys()，d.values(),d.items()得到的都是list对象
* 如果key不存在通过k["key"]来访问会报错，通过k.get()方法返回值为None不会报错。