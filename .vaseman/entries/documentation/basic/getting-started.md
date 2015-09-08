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

### Link assets files:

This command will make a symlink to Phoenix assets in `www/media`

``` bash
php bin/console phoenix asset sync phoenix
```

> If you are in Windows, you must open `cmd.exe` or `powershell.exe` with administrator access to run this command. Or you can also use hard copy:

> `php bin/console asset sync phoenix  --hard`

# Generate A New Package

Please make sure you have correct database configuration, then please type:

``` bash
$ php bin/console muse init flower sakura.sakuras -sm
```

And you will see this result:

![img](https://cloud.githubusercontent.com/assets/1639206/9724699/858b4cf2-560e-11e5-9137-956532efdb2e.png)

Package `flower` has been auto generated. We must register this package too, add it in `src/Windwalker.php`:

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

Direct sub routing to package routing at `etc/routing.yml`:

``` yaml
# etc/routing.yml

#...

# Add this route
flower:
    pattern: /flower
    package: flower
```

OK, now we can open `http://localhost/{your_project}/www/flower/sakuras` in browser, you will see a sample admin UI.

![img](https://cloud.githubusercontent.com/assets/1639206/9724923/231ea408-5611-11e5-8448-ff29aa059306.png)

Use PHP built-in server:

``` bash
cd {your_project}/www
php -S localhost:8000
```

Now you can use `http://localhost:8000/flower/sakuras` to test your application.

# Debug Mode

Add `/dev.php` before your URL, Windwalker will start debug mode and provides a powerful debug console.

> `http://localhost:8000/dev.php/flower.sakuras`

![img](https://cloud.githubusercontent.com/assets/1639206/9725055/0cc4e1fc-5613-11e5-9f0d-c373d7d68c87.png)


