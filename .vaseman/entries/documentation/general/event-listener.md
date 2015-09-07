layout: documentation.twig
title: Event Listener

---

# Introduction

Joomla has it's plugin system, and we can add our plugins into Joomla's Dispatcher without creating new plugins.

# Create Our EventListener

Windwalker will auto register linteners in `src/Flower/Listener/{Listener}/{Listener}.php`.

Now we can create a new Listener class:

``` php
<?php

namespace Flower\Listener\MyListener;

/**
 * Class MyListener
 */
class MyListener extends \JEvent
{
	public function onContentPrepare($context, $article, $params, $page = 0)
	{
		// Do some stuff
	}
}
```

Now this listener will auto inject to our plugin list. Everywhere call `onContentPrepare` will raise our listener to do something.

# Raise Event

``` php
$container = Container::getInstance('com_flower');

$dispatcher = $container->get('event.dispatcher');

$dispatcher->trigger('onContentPrepare', array('foo.bar', $article));
```

# ListenerHelper

We can use `ListenerHelper` to attach or detach listener to dispatcher.

## Attach Listener

``` php
\Windwalker\Event\ListenHelper::attach(new SakuraListener);
```

Attatch to particular dispatcher.

``` php
\Windwalker\Event\ListenHelper::attach(new SakuraListener, $dispatcher);
```

## Detach

Using linstener class name to detach a plugin.

``` php
\Windwalker\Event\ListenHelper::detach('Flower\\Listener\\MyListener\\MyListener');
```

