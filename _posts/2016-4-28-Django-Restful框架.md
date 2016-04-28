---
layout: post
title: Django-Resstful框架笔记
category: 技术
comments: true
---
###1.准备工作
* 安装django框架
* 安装django-rsetful 框架
```
pip install djangorestframework
```
###2.一个小demo
####2.1创建django工程
    django admin startproject restful
	django admin startapp demo
####2.2配置restful环境
    修改restful/settings.py
	在INSTALLED_APPS 添加 'rest_framework'
####2.3编写model层 /demo/model.py
    from django.db import models

	# Create your models here.
	class User(models.Model):
	    username = models.CharField(max_length=20,blank=True)
	    password = models.CharField(max_length=20,blank=True)
	    def __str__(self):
	        return self.username
####2.4配置数据库
    python manage.py makemigratons
	python manage.py migrate
	python manage.py createsuperuser
####2.5配置后台管理 /demo/admin.py
	from django.contrib import admin
	# Register your models here.
	from demo.models import User
	
	admin.site.register(User)
此时登陆后台添加一些数据

####2.6
	




