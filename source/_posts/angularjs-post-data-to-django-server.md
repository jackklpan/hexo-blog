---
title: angularjs post data to django server
tags:
  - angularjs
  - django
  - python
date: 2015-10-18 15:25:00
---

**Angularjs:**
var my_app = angular.module('MyApp').config(function($httpProvider) {
&nbsp; &nbsp; $httpProvider.defaults.headers.common['X-Requested-With'] = 'XMLHttpRequest';
&nbsp; &nbsp; $httpProvider.defaults.xsrfCookieName = 'csrftoken';
&nbsp; &nbsp; $httpProvider.defaults.xsrfHeaderName = 'X-CSRFToken';
});

$http.post('url', {
&nbsp; &nbsp; &nbsp; &nbsp; data: $scope.data
&nbsp; &nbsp; }).success(function(data) {
&nbsp; &nbsp; &nbsp; &nbsp; console.log(data);
&nbsp; &nbsp; }).error(function(e) {
&nbsp; &nbsp; &nbsp; &nbsp; console.log(e);
&nbsp; &nbsp; });

**Django:**
from django.http import HttpResponseBadRequest
from django.http import JsonResponse
import json

def post(request):
&nbsp; &nbsp; if not request.is_ajax():
&nbsp; &nbsp; &nbsp; &nbsp; return HttpResponseBadRequest('Expected an XMLHttpRequest')
&nbsp; &nbsp; in_data = json.loads(request.body.decode('utf-8'))
&nbsp; &nbsp;&nbsp;return JsonResponse({'status':'success'})