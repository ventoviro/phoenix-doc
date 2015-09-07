layout: documentation.twig
title: Curl Helper

---

# Introduction

In Joomla, we have a [Http](https://github.com/joomla-framework/http) package to send HTTP request, including CURL. But this class cannot customize some options we want, so we can using `CurlHelper` to handle our customize request.

# Original Joomla Http Object

``` php
// Create an instance of a default JHttp object.
$http = new JHttp;

$options = new JRegistry;

$transport = new JHttpTransportStream($options);

// Create a 'stream' transport.
$http = new JHttp($options, $transport);
```

Or using `JHttpFactory`

``` php
// Create an instance of a default JHttp object.
$http = JHttpFactory::getHttp();

// Invoke the HEAD request.
$response = $http->head('http://example.com');

// Prepare the data.
$data = array('make' => 'Holden', model => 'EJ-Special');

// Invoke the POST request.
$response = $http->post('http://api.example.com/cars/1', $data);

// Invoke the PUT request.
$response = $http->put('http://api.example.com/cars/1', $data);

// Invoke the DELETE request.
$response = $http->delete('http://api.example.com/cars/1');
```

## Respond object

``` php
var_dump($response->code);
```

The response code is included in the "code" property.
See http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html

``` php
var_dump($response->headers);
```

The response headers are included as an associative array in the "headers" property.


``` php
var_dump($response->body);
```

The body of the response (not applicable for the HEAD method) is included in the "body" property.

# CurlHelper

## getPage

``` php
$url = 'http://tw,yahoo.com';

$respond = \Windwalker\Helper\CurlHelper::get($url);

echo $respond->body;
```

## Post Page

``` php
$query = array(
    'foo' => 'bar'
);

$respond = \Windwalker\Helper\CurlHelper::get($url, 'post', $query);

echo $respond->body;
```

## Customize Options

``` php
$option = array(
    CURLOPT_USERAGENT => "Mozilla/5.0 (Windows NT 6.1; WOW64)",
	CURLOPT_FOLLOWLOCATION => !ini_get('open_basedir') ? true : false
);

$respond = \Windwalker\Helper\CurlHelper::get($url, 'get', $option);

echo $respond->body;
```

## Download File

``` php
$url = 'http://somewebsite.com/files/file.pdf';

$dest = JPATH_ROOT . '/files/newFile.pdf';

$option = array();

\Windwalker\Helper\CurlHelper::download($url, $dest, $option);
```



