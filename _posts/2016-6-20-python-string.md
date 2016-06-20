#python-String
##简介
* String是一个有序的字符集合。
* String中的元素是不可更改的
##操作符
	In [23]: "David"
	Out[23]: 'David'
	
	In [24]: name = "David"
	
	In [25]: name[3]
	Out[25]: 'i'
	
	In [26]: name*2
	Out[26]: 'DavidDavid'
	
	In [27]: name
	Out[27]: 'David'
	
	In [28]: len(name)
	Out[28]: 5

##函数
![](http://simplebrightman.github.io/blog/images/python/3.JPG)

	In [29]: name.center(20)
	Out[29]: '       David        '
	
	In [30]: name.count('a')
	Out[30]: 1
	
	In [31]: name.ljust(20)
	Out[31]: 'David               '
	
	In [32]: name.rjust(20)
	Out[32]: '               David'
	
	In [33]: name.upper()
	Out[33]: 'DAVID'
	
	In [34]: name.upper().lower()
	Out[34]: 'david'
	
	In [35]:
	In [35]: name.find('a')
	Out[35]: 1
	
	In [36]: name.split('a')
	Out[36]: ['D', 'vid']
	
	In [37]:
	In [37]: name[0] = 'a'
	---------------------------------------------------------------------------
	TypeError                                 Traceback (most recent call last)
	<ipython-input-37-31bd2df005af> in <module>()
	----> 1 name[0] = 'a'
	
	TypeError: 'str' object does not support item assignment

##与list的相互转化
	In [38]: strList = list(name) #name="David" string转lsit

	In [39]: strList
	Out[39]: ['D', 'a', 'v', 'i', 'd']
	
	In [40]: "".join(strList) #list转string
	Out[40]: 'David'