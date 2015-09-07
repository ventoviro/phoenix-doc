layout: documentation.twig
title: Html Builder

---

# Introduction

This is a convenience class to create a HTML in OO way.

# HtmlElement

``` php
use Windwalker\Html\HtmlElement;

$attrs = array(
    'class' => 'btn btn-mini',
    'onclick' => 'return false;'
);

$html = (string) new HtmlElement('button', 'Click', $attrs);
```

Then we will get this HTML:

``` html
<button class="btn btn-mini" onclick="return false;">Click</button>
```

## Get Attributes by Array Access

``` php
$class = $html['class'];
```

# HtmlElements

It is a collection of HtmlElement set.

``` php
$html = new HtmlElements(
    array(
        new HtmlElement('p', $content, $attrs),
        new HtmlElement('div', $content, $attrs),
        new HtmlElement('a', $content, $attrs)
    )
);

echo $html;
```

OR we can iterate it:

``` php
foreach ($html as $element)
{
    echo $element;
}
```


