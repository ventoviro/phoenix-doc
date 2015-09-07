layout: documentation.twig
title: Extension Helper

---

# Detect Extension Type

We can using a element name with prefix of Joomla extension, eg: `com_content` or `mod_menus` to detect what extension type is.

``` php
$extracted = \Windwalker\System\ExtensionHelper::extractElement('com_content');

print_r($extracted);

$extracted = \Windwalker\System\ExtensionHelper::extractElement('plg_systemdebug');

print_r($extracted);
```

The result will be:

```
Array
    (
        [type]  => component
        [name]  => content
        [group] => null
    )

Array
    (
        [type]  => plugin
        [name]  => debug
        [group] => system
    )
```

# Get Extension Params

We have a `JComponentHelper::getParams()` can help us get params of component now, but there is not so convience for modules and plugins. `ExtensionHelper::getParams()` will do this quickly.

``` php
$params = \Windwalker\System\ExtensionHelper::getParams('com_content');

$params = \Windwalker\System\ExtensionHelper::getParams('mod_menus');

$params = \Windwalker\System\ExtensionHelper::getParams('plg_system_cache');
```
