---
title: "django (un)chained by way of oops"
categories:
  - blog
tags:
  - update
---

I was stalking Django's Trac forum and stumbled into a pair of related tickets that took me surprisingly deep into the ORM. 
So I reread the documentation (it's been a couple years), refresher below.

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
    * manager is "the main source of QuerySets for a model"; lots of stuff I skipped here
* A QuerySet is ... 
  * a lazily evaluated collection of objects from the database [which is lazily evaluated](https://docs.djangoproject.com/en/5.0/topics/db/queries/#querysets-are-lazy)
  * ... equivalent to a [SQL query](https://docs.djangoproject.com/en/5.0/topics/db/queries/#retrieving-objects) 
    * methods such as `filter()`, `exclude()`, `get()`  are how filters are added to a basic SELECT 
    * lots of convenience methods here such as 
      * [pk lookup shortcut](https://docs.djangoproject.com/en/5.0/topics/db/queries/#the-pk-lookup-shortcut) e.g. `Blog.objects.get(pk__in=[])`
      * [lookups that span relationships](https://docs.djangoproject.com/en/5.0/topics/db/queries/#lookups-that-span-relationships) e.g. `Blog.objects.filter(entry__authors__isnull=False, entry__authors__name__isnull=True)`
  * [cached](https://docs.djangoproject.com/en/5.0/topics/db/queries/#caching-and-querysets) once a database query happens, *most of the time*
* A [query expression](https://docs.djangoproject.com/en/5.0/ref/models/expressions/) is an extension of a queryset; I quote...
  * describe a value or a computation that can be used as part of an update, create, filter, order by, annotation, or aggregate ... 
  * a number of built-in expressions e.g. `.aggregate()`, `annotate()`, `filter(Q())` (which I [previously abused in a take home](https://github.com/sharonwoo/grant-household-api-docker/blob/main/household-api/api/views.py))
  * even window functions
  * ... `Value()`
  * **these take an optional `output_field` [which if not specified needs to be inferred](https://docs.djangoproject.com/en/5.0/ref/models/querysets/#output-field); understanding this (which I had never used before) was the crux of my tickets**

