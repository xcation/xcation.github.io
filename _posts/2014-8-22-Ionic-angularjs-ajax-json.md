---
layout: post
title: AngularJS ajax
category: Ionic
tags: Python
description: Ionic Framework Use AngularJS
---

## Ionic Framework 是移动应用开发框架,HTML5 移动端应用框架，使用 HTML5 开发混合移动应用前端框架。支持app 打包，android　与　ＩＯＳ。


Ioniｃ　angularjs post get put jquery ajax 方式

## 配置代码，在入口JS加入

        angular.module('App', [])

        .config(function($stateProvider, $urlRouterProvider, $httpProvider) {

           

            $httpProvider.defaults.headers.put['Content-Type'] = 'application/x-www-form-urlencoded';
            $httpProvider.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded';
         
            // Override $http service's default transformRequest
            $httpProvider.defaults.transformRequest = [function(data) {
                /**
                 * The workhorse; converts an object to x-www-form-urlencoded serialization.
                 * @param {Object} obj
                 * @return {String}
                 */
                var param = function(obj) {
                    var query = '';
                    var name, value, fullSubName, subName, subValue, innerObj, i;
         
                    for (name in obj) {
                        value = obj[name];
         
                        if (value instanceof Array) {
                            for (i = 0; i < value.length; ++i) {
                                subValue = value[i];
                                fullSubName = name + '[' + i + ']';
                                innerObj = {};
                                innerObj[fullSubName] = subValue;
                                query += param(innerObj) + '&';
                            }
                        } else if (value instanceof Object) {
                            for (subName in value) {
                                subValue = value[subName];
                                fullSubName = name + '[' + subName + ']';
                                innerObj = {};
                                innerObj[fullSubName] = subValue;
                                query += param(innerObj) + '&';
                            }
                        } else if (value !== undefined && value !== null) {
                            query += encodeURIComponent(name) + '='
                                    + encodeURIComponent(value) + '&';
                        }
                    }
         
                    return query.length ? query.substr(0, query.length - 1) : query;
                };
         
                return angular.isObject(data) && String(data) !== '[object File]'
                        ? param(data)
                        : data;
            }]



    

###在controllers.js 就可以如下处理：

        $http({
            method: 'POST',
            url: url,
            data:postDate,
            headers: {
                'Content-Type': 'application/x-www-form-urlencoded; charset=utf-8'
            }
            
        })

            .success(function(data, status, headers, config) {
                console.log(data.username);
                            
                
            })
            .error(function(data, status, headers, confignseData) {
                console.log("网络链接");
                
            });

     
    


