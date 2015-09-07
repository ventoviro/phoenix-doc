layout: documentation.twig
title: Path Helper

---

# Introduction

Sometimes we using `JPATH_COMPONENT` to get component path, however, this constant is dynamic, we can;t use this constant in a component to get other component's path.

`PathHelper` can get extensions' real path by the element name.

# Get Path

## Get Component Path

``` php
echo \Windwlaker\Helper\PathHelper::get('com_content', 'admin');

// /your/path/to/joomla/administrator/components/com_content

echo \Windwlaker\Helper\PathHelper::get('com_content', 'site');

// /your/path/to/joomla/components/com_content
```

## Get Module Path

``` php
echo \Windwlaker\Helper\PathHelper::get('mod_menus', 'admin');

// /your/path/to/joomla/administrator/modules/mod_menus

echo \Windwlaker\Helper\PathHelper::get('mod_menus', 'site');

// /your/path/to/joomla/modules/mod_menus
```

## Get Plugin Path

``` php
// Plugin only in site
echo \Windwlaker\Helper\PathHelper::get('plg_system_cache');

// /your/path/to/joomla/plugins/system/cache
```

## Get Template Path

``` php
echo \Windwlaker\Helper\PathHelper::get('tpl_isis', 'admin');

// /your/path/to/joomla/administrator/templates/isis

echo \Windwlaker\Helper\PathHelper::get('tpl_protostar', 'site');

// /your/path/to/joomla/templates/protostar
```

# getAdmin() & getSite()

This is the alias of `get($ext, 'admin')`, `get($ext, 'site')`.
