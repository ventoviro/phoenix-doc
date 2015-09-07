layout: documentation.twig
title: Xml Helper

---

# Introduction

`XmlHelper` is use to get attributes of `SimpleXmlElement`.

# Get Attributes

``` php
use Windwalker\Helper\XmlHelper;

$xml = <<<XML
<root>
    <field name="foo" type="bar" readonly="true">
        <option></option>
    </field>
</root>
XML;

$xml = simple_xml_load_string($xml);

$element = $xml->xpath('field');

$name = XmlHelper::getAttribute($element, 'name'); // result: foo

// Same as get()
$name = XmlHelper::get($element, 'name'); // result: foo
```

# Get Boolean

`getBool()` can help us convert some string link `true`, `1`, `yes` to boolean `TRUE` and `no`, `false`, `disabled`, `null`, `none`, `0` string to booleand `FALSE`.

``` php
$bool = XmlHelper::getBool($element, 'readonly'); // result: (boolean) TRUE
```

# Get False

Just an alias of `getBool()` but FALSE will return `TRUE`.

# Set Default

If this attribute not exists, use this value as default, or we use original value from xml.

``` php
XmlHelper::def($element, 'class', 'input');
```


