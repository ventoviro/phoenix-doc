layout: documentation.twig
title: Html Helper

---

# Repair Tags

We can using `repair()` method to repair unpaired tags by `php tidy`, if tidy extension not exists, will using simple tag close function to fix it.

``` php
$html = '<p>foo</i>';

$html = \Windwalker\Helper\HtmlHelper::repair($html);

echo $html; // <p>foo</p>
```

# Get JS Object

This method convert a nested array or object to JSON format that you can inject it to JS code.

``` php
$option = array(
    'url' => 'http://foo.com',
    'foo' => array('bar', 'yoo')
);

echo $option = \Windwalker\Helper\HtmlHelper::getJSOBject($option);
```

Result

```
{
    "url" : "http://foo.com",
    "foo" : ["bar", "yoo"]
}
```



