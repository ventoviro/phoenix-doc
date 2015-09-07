layout: documentation.twig
title: JContent Helper

---

# Introduction

`JContentHelper` is a simple helper to get some Joomla content component information.

# Get Article Link

``` php
echo \Windwalker\Helper\JContent::getArticleLink('35:alias-link-url', 7);
```

Retun this URL: `category/subcategory/35-alias-link-url.html`

Same as this code:

``` php
include_once JPATH_ROOT.'/components/com_content/helpers/route.php' ;

echo JRoute::_(ContentHelperRoute::getArticleRoute($slug, $catslug));
```

# Get Category Link

``` php
echo \Windwalker\Helper\JContentHelper::getCategoryLink(11);
```

Return: `category.html`

Same as:

``` php
include_once JPATH_ROOT.'/components/com_content/helpers/route.php' ;

echo JRoute::_(ContentHelperRoute::getCategoryRoute($catid));
```
