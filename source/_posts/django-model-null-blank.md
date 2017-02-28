---
title: django model null blank
tags:
  - django
date: 2015-10-18 15:28:00
---

django default is not null.
If we allow null value, add null=true option in model.
However, for&nbsp;CharField and TextField, we should not add it, because empty string ('') already represent null value.
In addition, set null=true means we also need to set blank=true.
Because in django, null controls the database setting; blank controls the form setting. So we need to set blank=true to allow the from field to be empty.

https://docs.djangoproject.com/en/1.8/ref/models/fields/#django.db.models.Field.null