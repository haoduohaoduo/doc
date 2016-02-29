# Angular 规范要点

我们的规范主要以 https://github.com/johnpapa/angular-styleguide/blob/master/a1/i18n/zh-CN.md 为基础。下面是本次重构中着重修改的：

## 使用 ngAnnotate，不手写 Angular 的依赖注入

为了让代码在 uglify 之后还能运行，我们要手写 Angular 的依赖注入，像这样：

    SomeController.$inject = ['$scope', ...];
    function SomeController($scope, ...) {
      ...
    }
    
每个 service 都要写两遍，如果依赖的 service 比较多，这样写非常容易出错。

使用 Grunt 的 ngAnnotate 插件可以帮我们完成这个步骤，所以我们只需要这样写就可以了：
    
    function SomeController($scope, ...) {
      ...
    }

ngAnnotate 会自动帮我们加上 `SomeController.$inject = ['$scope', ...];`

## 写依赖注入的时候，把 Angular 内置的服务写在前面，第三方的服务写在后面，自己写的放在最后。
   
    // BAD
    function SomeController(N, $http, DS, ModelService, $scope) {
      ...
    }
    
    //GOOD
    function SomeController($scope, $http, DS, N, ModelService) {
      ...
    }
    
## route参数
route中的id类参数写清全称，如xxxID，不简化为id，同样的id，名称要统一：

    // GOOD
    $routeProvider.when('/product/:productID', {
      templateUrl: 'views/product/product.html',
      controller: 'ProductCtrl'
    })
    
    //BAD
    $routeProvider.when('/product/:id', {
      templateUrl: 'views/product/product.html',
      controller: 'ProductCtrl'
    })
    
route中有多个参数时，更应该区分：
    
    //GOOD
    .when('/pos-content/:positionID/position/:posContentID', {
      templateUrl: 'views/position/pos-content.html',
      controller: 'PosContentCtrl'
    })
    
    //BAD
    .when('/pos-content/:id/position/:pid', {
      templateUrl: 'views/position/pos-content.html',
      controller: 'PosContentCtrl'
    })
    
 相应地，要在controller开头中，将route参数定义为常量，名称写全，不要简化为ID或者其他名称
 
     //GOOD
     function PosContentsCtrl($scope, $routeParams) {

       var vm = $scope;
       var POSITION_ID = $routeParams.positionID || null;
       ...
     }
     
     //BAD
     function PosContentsCtrl($scope, $routeParams) {

       var vm = $scope;
       var id = $routeParams.positionID || null;
       ...
     }
     
     //BAD
     function PosContentsCtrl($scope, $routeParams) {

       var vm = $scope;
       var PID = $routeParams.positionID || null;
       ...
     }

## 为了不暴露全局变量，应将每一段代码用立即执行函数包裹。`'use strict'` 写在函数内部（原因：http://www.ruanyifeng.com/blog/2013/01/javascript_strict_mode.html）
    
    //GOOD
    (function(){
    	'use strict';
    
      angular.module('app').controller('SomeController', SomeController)
      
      function SomeController($scope, ...) {
        ...
      }
    })()
    
    //BAD
    angular.module('app').controller('SomeController', SomeController)
      
    function SomeController($scope, ...) { //这个函数会暴露到全局
      ...
    }

