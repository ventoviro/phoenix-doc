layout: documentation.twig
title: Thumb

---

# Introduction

`Image\Thumb` is a wrap of `JImage`, we can quickly generate image thumb and return url to use.

# Create Thumb Object

``` php
$config = new JRegistry;

$extension = 'com_flower';

$thumb = new \Windwalker\Image\Thumb($config, $extension);
```

First params `$config` is to set some path of cache:

- `path.cache`
- `path.temp`
- `url.cache`
- `url.temp`

`$extension` means we can get config from this extension options. `Thimb` class will using `ExtensionHelper` to get params of this extension and merge to Thumb config.

## Config in Extension XML

Using this xml in your `config.xml`.

``` xml
<fields name="thumb">
    <field name="cache-path"
        type="text"
        label="Thumb Cache Path"
        />

    <field name="temp-path"
        type="text"
        label="Thumb Temp Path"
        />

    <field name="cache-url"
        type="text"
        label="Thumb Cache URL"
        />

    <field name="temp-url"
        type="text"
        label="Thumb Temp URL"
        />
</fields>
```

# Create Image Thumb

## Resize

``` php
$img = 'http://yoursite.com/images/image.png';

echo $thumb->resize($img, 150, 150);
```

## Resize & Crop

``` php
echo $thumb->resize($img, 150, 150, \JImage::CROP_RESIZE);
// or
echo $thumb->resize($img, 150, 150, true);
```

## Resize & Crop Methods

```
\JImage::SCALE_FILL
\JImage::SCALE_INSIDE
\JImage::SCALE_OUTSIDE
\JImage::CROP
\JImage::CROP_RESIZE
\JImage::SCALE_FIT
```

## Quality

Add quality (max is 100) to 5th param.

``` php
echo $thumb->resize($img, 150, 150, \JImage::CROP_RESIZE, 95);
```

# ThumbHelper

## Resize

`ThumbHelper` can quickly generate thumbs:

``` php
echo \Windwalker\Image\ThumbHelper::resize($img, 150, 150, \JImage::SCALE_INSIDE);
```

Same as:

``` php
$thumb = new \Windwalker\Image\Thumb(null, 'lib_windwalker');
$thumb->resize($img, 150, 150, \JImage::SCALE_INSIDE);
```

## getInstance

If we use this method to generate new object, it will be stored as singleton.

``` php
$thumb = ThumbHelper::getIbstance('com_flower', new JRegisrty);
```

