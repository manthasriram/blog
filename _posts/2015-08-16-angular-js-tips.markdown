---
layout:     post
title:      "Angular js"
subtitle:   "Angular JS tips and tricks"
date:       2015-08-16 12:00:00
author:     "Sriram Mantha"
---

#Logging in AngularJS. Test

Here are an example on how you could enable logging in angularjs

Enable logging to the preferred level

```javascript
//Enable Debug logging
angular.module("app-config-ui").config(function($logProvider){
  $logProvider.debugEnabled(true);
});
```

inject the logger dependency and log the debug message

``` javascript
angular.module('logExample', [])
.controller('LogController', ['$scope', '$log', function($scope, $log) {
  $scope.$log = $log;
  $scope.message = 'Hello World!';
  $log.debug("My Debug Message")
}]);
```


#Using ng-class

Usage

``` javascript
 ng-class="{ 'class': expr}"
```

Provide an expression to evaluate the class conditionally

Example

``` javascript
 ng-class="{'caret': menu.subMenus && menu.subMenus.length > 0}"
```


#Evaluating dynamic Html's

You often add html code to your webpage dynamically through javascript code. 
You will need to compile the html using angular's $compile function for angular to evaluate the dynamic code

For example you add

``` javascript
$('<td/>').html("<div ng-model="name"> </div>")
```

More documentation can be found here



#Modal window using UI bootstrap

Bootstrap and angular do not work that well together and hence the UI-Bootstrap angular module.

Install angular bootstrap to your app by 
bower install angular-bootstrap

Add ui-bootstrap as a dependency to your angular app

``` javascript
var mainApp = angular.module("mainApp", ['ngRoute', 'ngResource', 'ui.bootstrap', 'appcore']);
```

To programmatically  invoke a modal window here is the code snippet

You can pass in a controller too to handle the modal function

``` javascript
  var modalInstance = $modal.open({
                    scope: $scope,
                    controller: 'ModalController',
                    templateUrl: 'lModal.html',
                    size: 'lg',
                    resolve: {
                        gridDetailId: function() {
                            return gridDetailId;
                  }
           }
  });

angular.module('app-config-ui').controller(
    'ModalController',
    function($scope, $log, $resource, $modalInstance, gridDetailId) {
});
```


#Select html element using ng-options

Here are a few tips and tricks for a html select element

``` javascript
<select class='form-control' ng-model='selectedval' 
 ng-options='item.id as item.name for item in options' ng-required='required'><option value=''>-- select --</option></select>
```

Displays by the name attribute on the select field and matches the model value with the id field

The selectedVal will be "1" or "2" based on the below data model

Data model

``` javascript
$scope.options = [{"id":"1","name":"apple"},{"id":"2","name":"orange"}];
```