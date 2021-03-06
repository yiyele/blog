---
layout: post
title: Django-Restful框架
category: 技术
comments: true
---
##1.准备工作
* 官方文档：[http://www.django-rest-framework.org/](http://www.django-rest-framework.org/)
* 安装django框架
* 安装django-rsetful 框架
```
pip install djangorestframework
```

##2.一个小demo
###2.1创建django工程
```python

    django admin startproject restful
	django admin startapp demo
```
###2.2配置restful环境
```python

    修改restful/settings.py
	在INSTALLED_APPS 添加 'rest_framework'
```
###2.3编写model层 /demo/model.py
```python

    from django.db import models

	# Create your models here.
	class User(models.Model):
	    username = models.CharField(max_length=20,blank=True)
	    password = models.CharField(max_length=20,blank=True)
	    def __str__(self):
	        return self.username
```
###2.4配置数据库
```python

    python manage.py makemigratons
	python manage.py migrate
	python manage.py createsuperuser
```
###2.5配置后台管理 /demo/admin.py
```python

	from django.contrib import admin
	# Register your models here.
	from demo.models import User
	
	admin.site.register(User)
```
此时登陆后台添加一些数据
![](http://simplebrightman.github.io/blog/images/django-restful/AddUser.jpg)
(图片不清楚可按住Ctrl+鼠标滚轮放大)
###2.6编写序列化模块 /demo/serializer.py
```python

	# author: HuYong
	# coding=utf-8
	from rest_framework import serializers
	
	from demo.models import User
	
	
	class UserSerializer(serializers.ModelSerializer):
	    class Meta:
	        model = User
	        fields = ("id","username","password")
```
	
序列化联通json与模型层
###2.7编写url
####2.7.1根url  restful/url.py
```python

	from django.conf.urls import include, url
	from django.contrib import admin
	
	urlpatterns = [
	    url(r'^admin/', include(admin.site.urls)),
	    url(r'^api/demo/',include('demo.urls')),
	]
```
####2.7.2APP URL　demo/urls.py
```python

	# author: HuYong
	# coding=utf-8
	from django.conf.urls import url
	
	from demo import views
	
	urlpatterns = [
	    url(r'^user/$',views.User_list),
	    url(r'^user/(?P<pk>[0-9]+)/$',views.User_detial),
	]
```
###2.8编写views层 demo/views.py
```python

	import json
	
	from django.shortcuts import render
	
	# Create your views here.
	from rest_framework import status
	from rest_framework.decorators import api_view
	from rest_framework.response import Response
	
	from demo.models import User
	from demo.serializer import UserSerializer
	
	
	@api_view(['GET','POST'])
	def User_list(request):
	
	    if request.method=="GET":
	        users = User.objects.all()
	        serializer = UserSerializer(users,many=True)
	        return Response(serializer.data)
	
	    elif request.method == 'POST':
	        print request.body
	        serializer = UserSerializer(data=json.loads(request.body))
	        if serializer.is_valid():
	            serializer.save()
	            return Response(serializer.data, status=status.HTTP_201_CREATED)
	        else:
	            return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)
	
	
	@api_view(['GET', 'PUT', 'DELETE']) #
	def User_detial(request,pk):
	    try:
	        user = User.objects.get(pk=pk)
	    except User.DoesNotExist:
	        return Response(status=status.HTTP_404_NOT_FOUND)
	
	    if request.method == "GET":
	        serializer = UserSerializer(user)
	        return Response(serializer.data)
	
	    elif request.method == "PUT":
	        serializer = UserSerializer(user,data=json.loads(request.body))
	        if serializer.is_valid():
	            serializer.save()
	            return Response(serializer.data)
	        else:
	            return Response(serializer.errors,status=status.HTTP_400_BAD_REQUEST)
	
	    elif request.method == "DELETE":
	        user.delete()
	        return Response(status=status.HTTP_204_NO_CONTENT)
```
###2.9测试
####2.9.1获取用户列表
* 浏览器访问http://127.0.0.1:8000/api/demo/user/
![](http://simplebrightman.github.io/blog/images/django-restful/User_List.jpg)
这个浏览器访问的界面
* 通过postman来测试，返回的是json数据
![](http://simplebrightman.github.io/blog/images/django-restful/User_List_Json.JPG)
####2.9.2新增数据
* 通过postman来测试
* 简单设置
![](http://simplebrightman.github.io/blog/images/django-restful/User_Post1.JPG)
![](http://simplebrightman.github.io/blog/images/django-restful/User_Post2.JPG)
* 返回的数据：
![](http://simplebrightman.github.io/blog/images/django-restful/User_Post3.JPG)
* 此时获取用户列表栏
![](http://simplebrightman.github.io/blog/images/django-restful/User_List2.JPG)
####2.9.3对单个用户的操作
* URL http://127.0.0.1:8000/api/demo/user/4   （id为4的用户）
* 获取用户信息（GET）
![](http://simplebrightman.github.io/blog/images/django-restful/User4_Get.JPG)
* 修改用户信息（PUT）
![](http://simplebrightman.github.io/blog/images/django-restful/User4_Put1.JPG)
![](http://simplebrightman.github.io/blog/images/django-restful/User4_Put2.JPG)
* 删除用户信息（DELETE）
![](http://simplebrightman.github.io/blog/images/django-restful/User4_Delete.JPG)
##3.基于APIVIEW重写view层
###3.1重写view层 /demo/views.py
```python 

	import json
	from django.shortcuts import render
	
	# Create your views here.
	from rest_framework import status
	from rest_framework.decorators import api_view
	from rest_framework.response import Response
	from rest_framework.views import APIView
	
	from demo.models import User
	from demo.serializer import UserSerializer
	
	
	class UserList(APIView):
	    def get(self,request,format=None):
	        users = User.objects.all()
	        serializer = UserSerializer(users, many=True)
	        return Response(serializer.data)
	
	    def post(self,request,format=None):
	        serializer = UserSerializer(data=json.loads(request.body))
	        if serializer.is_valid():
	            serializer.save()
	            return Response(serializer.data, status=status.HTTP_201_CREATED)
	        else:
	            return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)
	
	
	
	class UserDetial(APIView):
	    def getObject(self,pk):
	        try:
	            return User.objects.get(pk=pk)
	        except User.DoesNotExist:
	            return Response(status=status.HTTP_404_NOT_FOUND)
	
	    def get(self,request,pk,format=None):
	        user = self.getObject(pk)
	        serializer = UserSerializer(user)
	        return Response(serializer.data)
	
	    def put(self,request,pk,format=None):
	        user = self.getObject(pk)
	        serializer = UserSerializer(user, data=json.loads(request.body))
	        if serializer.is_valid():
	            serializer.save()
	            return Response(serializer.data)
	        else:
	            return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)
	
	    def delete(self,request,pk,format=None):
	        user = self.getObject(pk)
	        user.delete()
	        return Response(status=status.HTTP_204_NO_CONTENT)

```
###3.2重写url demo/urls.py
```python

	# author: HuYong
	# coding=utf-8
	from django.conf.urls import url
	from rest_framework.urlpatterns import format_suffix_patterns
	
	from demo import views
	
	urlpatterns = [
	    url(r'^user/$',views.UserList.as_view()),
	    url(r'^user/(?P<pk>[0-9]+)',views.UserDetial.as_view()),
	]
	
	urlpatterns = format_suffix_patterns(urlpatterns)
```
###3.3测试
会有报错，在restful/setting.py中加入

```python

	APPEND_SLASH = False
```

之后测试正常。













