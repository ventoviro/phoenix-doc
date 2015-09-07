---

layout: documentation.twig
title: Getting Started

---

# Installation

Please install Windwalker Framework first. See [Windwalker Installation](http://windwalker.io/documentation/start/getting-started.html)

Then add `"windwalker/phoenix": "~1.0"` to require block and run `composer update`.

## Prepare Phoenix Package

Add Phoenix package object to `Windwalker/Windwalker::loadPackages()`.

``` php
// src/Windwalker.php

class Windwalker extends \Windwalker\Core\Windwalker
{
	public static function loadPackages()
	{
		return array(
			'system' => new SystemPackage,
			'phoenix' => new \Phoenix\PhoenixPackage // Add this line
		);
	}
	
	// ...
```

## Link assets files:

This command will make a symlink to Phoenix assets in `www/media`

``` bash
php bin/console phoenix asset sync phoenix
```

If you are in Windows, you must open `cmd.exe` or `powershell.exe` with administrator access to run this command. Or you may use hard copy:

``` bash
php bin/console asset sync phoenix  --hard
```

# Generate A New Package

Please make sure you have correct database configuration, then you can type:

``` bash
$ php bin/console muse init flower sakura.sakuras -sm
```

And you will see this result:

![p-2015-09-07-001](https://cloud.githubusercontent.com/assets/1639206/9719148/59a365c0-55b4-11e5-972a-0f316b0166f6.jpg)

We must add this package too, register it in `src/Windwalker.php`:

``` php
// src/Windwalker.php

class Windwalker extends \Windwalker\Core\Windwalker
{
	public static function loadPackages()
	{
		return array(
			'system' => new SystemPackage,
			'phoenix' => new \Phoenix\PhoenixPackage,
			'flower' => new \Flower\FlowerPackage  // Add this line
		);
	}
	
	// ...
```

Then create symlink to assets of this package:

``` bash
php bin/console asset sync flower [--hard]
```





# Generate Extensions

Here is some example of how to generate extensions:

## Init Component

Create a component named `com_flower` and with two MVCs `sakura` and `sakuras` in both site and admin.

``` bash
$ php bin/windwalker generator init com_flower sakura.sakuras
```

Create a component in site or admin.

``` bash
$ php bin/windwalker generator init com_flower sakura.sakuras -c admin (site)
```

Create a component and use other sub template `foo`, default is `default`.

``` bash
$ php bin/windwalker generator init com_flower sakura.sakuras -t foo
```

## Add two MVC groups

Add a singular and a plural MVC group to a exists component.

``` bash
$ php bin/windwalker generator add subsystem com_flower rose.roses
```

## Module

Create a module named `mod_flower` in front end.

``` bash
$ php bin/windwalker generator init mod_flower -c site
```

## Plugin

Create a module named `plg_flower` in 'system' group.

``` bash
$ php bin/windwalker generator init plg_system_flower
```

