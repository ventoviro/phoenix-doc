layout: documentation.twig
title: Uri Helper

---

# Base64 Handler

We provides a universal interface for url base64 encode and decode, please using this code to encode url:

``` php
echo \Windwalker\Helper\Uri::base64('encode', $url);
```

And using this to decode:

``` php
echo \Windwalker\Helper\Uri::base64('decode', $url);
```

> The `encode` action is same as `base64_encode()` function. But the `decode()` will make the url safe and replace `' '` to `'+'` to avoid decode error.

# Download and Stream

## Direct Download

Another method is `download()`, we can using redirect download by this code:

``` php
\Windwalker\Helper\Uri::download('files/file.pdf', true);
```

This will redirec to `{ROOT}/files/file.pdf` and download it.

## Stream Download

Using:

``` php
\Windwalker\Helper\Uri::download('files/file.pdf', true, true);
```

Will using stream to download a file, it is useful when we want to hide the real file url.

Note: Please don't flush or echo any character before stream downlaod, or these character will be included to this file and make file corrupted.
