# Sanitizr

Basic sanitizer class for PHP applications.

## Features

Sanitize an array of data to any set of rules.

## Methods

- All php text methods
- Custom methods

If you think about anything else that could be added, feel free to submit a PR on the develop branch.

## Install

Install this package through composer

```
composer require whatdafox/sanitizer
```

Create a class that extends `Sanitizer\Sanitizer` and create a property `rules` to indicate your rules

```php
<?php

use Sanitizer\Sanitizer;

class AcmeSanitizer extends Serializer {

    protected $rules = [
        'name' => 'trim|strtolower|ucwords',
        'email' => 'trim|strtolower'
    ];

}
```

To use your sanitizer, just call the `sanitize()` method with the array of data like so:

```php
<?php

$sanitizer = new AcmeSanitizer;

$data = [
    'name' => ' JOHN DOE  ',
    'email' => 'JOHNDOE@EXAMPLE.com  '
];

$data = $sanitizer->sanitize($data);

// returns
// [
//     'name' => 'John Doe',
//     'email' => 'johndoe@example.com'
// ]
```

## Custom sanitizers

If you would like to create your own sanitizing methods, just create a method with the `sanitize` prefix on your class like so: 

```php
public function sanitizeSnakeCase(){
    //
}
```

Then add `snakeCase` anywhere in your rules to use it!

## Use with Laravel

You can inject any Sanitizer class you will create as a dependency within a constructor or in a method in your Laravel controllers. 

Just typehint the class like so: 

```php
public function index(AcmeSanitizer $sanitizer) {
    //
}
```

You can also call the sanitize method automatically when Laravel is resolving the dependency, by using [Container Events](http://laravel.com/docs/5.0/container#container-events) in your Service Providers. For example: 

```php
$this->app->resolving(AcmeSanitizer::class, function($sanitizer, $app) {
    $app->request->merge($sanitizer->sanitize($app->request->all()));
});
```
*This example will apply the rules to the request data when resolving the injected sanitizer class, this way you do not have to call `sanitize()` yourself!*


That's all folks!

## Thanks

Thanks for Jeffrey Way and Laracasts for the inspiration and examples. http://laracasts.com
