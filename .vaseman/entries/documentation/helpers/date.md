layout: documentation.twig
title: Date Helper

---

# Using DateHelper

Use

``` php
$date = \Windwalker\Helper\DateHelper::getDate('now');
```

Same as

``` php
$dta = JFactory::getDate('now', JFactory::getConfig()->get('offset'));
```

To get the `JDate` object for local timezone.
