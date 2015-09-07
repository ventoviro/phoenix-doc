layout: documentation.twig
title: ReflectionHelper

---

# Introduction

In PHP we always using `Reflection` classes to get information of object or classes, but it's a little bother that we have to new Reflection object every time.

`ReflectionHelper` help us generate Reflection object and cache them, then we can use these Reflection objects when we need.

# Create Reflection

``` php
$ref = \Windwalker\Helper\ReflectionHelper::getReflection('JController');

$ref->getFilename(); // Get file path of this class.
```

# Using Magic Method to call ReflectionClass Methods

`ReflectionHelper` can use any methods of [ReflectionClass](http://www.php.net/manual/en/class.reflectionclass.php).

``` php
use Windwalker\Helper\ReflectionHelper;

ReflectionHelper::getMethods('JController');

ReflectionHelper::isAbstract('JController');

ReflectionHelper::hasConstant('JController', 'FOO');
```





