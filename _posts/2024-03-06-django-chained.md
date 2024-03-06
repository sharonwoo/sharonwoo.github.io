---
title: "hello world"
categories:
  - blog
tags:
  - update
---

I was stalking Django's Trac forum and stumbled into a pair of related tickets that took me surprisingly deep into the ORM. 

## Queryset 

Per the documentation: 
* A model is a database table 
* Each model has at least 1 [Manager](https://docs.djangoproject.com/en/5.0/topics/db/managers/#django.db.models.Manager), 
  * a manager is the interface through which database query operations are provided to Django models, it's part of the model class
  * the default manager name is `objects`; [django/db/models/manager.py](https://github.com/django/django/blob/main/django/db/models/manager.py)
    * so `Model.objects.all()` returns all rows in the `Model` table 
  * [managers can be customized](https://docs.djangoproject.com/en/5.0/topics/db/managers/#modifying-a-manager-s-initial-queryset)
  * each manager has a base queryset which can be overridden by overriding `get_queryset()` (`all()` calls `get_queryset()` so also goes)
    * `get_queryset()` returns a QuerySet object so those methods can be invoked
    * manager is "the main source of QuerySets for a model"
* A QuerySet is ...
  * a collection of objects from the database [which is lazily evaluated](https://docs.djangoproject.com/en/5.0/topics/db/queries/#querysets-are-lazy)
  * ... equivalent to a [SQL query](https://docs.djangoproject.com/en/5.0/topics/db/queries/#retrieving-objects) that can take filters
    * such as `filter()`, `exclude()`, `get()` 
    * [pk lookup shortcut](https://docs.djangoproject.com/en/5.0/topics/db/queries/#the-pk-lookup-shortcut) e.g. `Blog.objects.get(pk__in=[])`

