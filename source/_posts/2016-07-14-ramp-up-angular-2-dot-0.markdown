---
layout: post
title: "Ramp Up Angular 2.0"
date: 2016-07-14 02:29:53 +0000
comments: true
categories: Angular
---

First Things:

### Download Angular
URL: [Angular](http://angularjs.org)
We'll need angular.min.js

### Download BootStrap
URL: [BootStrap](http://getbootstrap.com)
also bootstrap.min.css


### Ramp up

``` html index.html
<!DOCTYPE html>
<html>
  <head>
    <link rel="stylesheet" type="text/css" href="bootstrap.min.css" />
    <script type="text/javascript" src="angular.min.js"></script>
    <script type="text/javascript" src="app.js"></script>
  </head>
  <body>
    <h1></h1>
  </body>
</html>
``` 

#### Create a Store Module

``` js app.js
var app;
var app = angular.module("gemStore",[]);
```

#### Attach module to HTML Pages

**KeyWords** `ng-app`

``` html
<html ng-app="gemStore">
...
</html>
```

#### Create a controller

``` js app.js
(function(){
  var gem = { name: 'Azurite', price: 2.95 };
  var app = angular.module('gemStore', []);
  app.controller('StoreController', function(){

  });
})();
```

#### Attach Controller on HTML page and alias it to other name

**KeyWords** `ng-controller`

``` html
<body ng-controller="StoreController as store">
</body>
```

Added a `gem` object to represent one of the products in our `gemStore`.
Assign it to the `product` property of `"StoreController`

``` js
  app.controller('StoreController', function(){
    this.product = gem;
  });
```

#### Display name on the HTML

``` html
<div class="product row">
      <h3>
        {{store.product.name}}
        <em class="pull-right">{{store.product.price}}</em>
      </h3>
</div>
```

#### Show or Hide

``` html
<button ng-show="store.product.canPurchase">Add to Cart</button>
```

If the canPurchase equal `true`, the Button should be display on pages.

``` html
<div class="product row" ng-hide="store.product.soldOut">

</div>
```

#### More Gems

``` js app.js
  app.controller('StoreController', function(){
    this.products = gems;
  });

```

**KeyWords** : `s`

And change the HTML code

``` html
<div class="product row" ng-repeat="product in store.products">
```

**KeyWords** `ng-repeat`