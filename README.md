# Sanitizr

Basic sanitizer class for PHP applications.

## Features

Sanitize an array of data to any set of rules.

## Methods

- All php text methods

If you think about anything else that could be added, feel free to submit a PR on the develop branch.

## Install

Install this package through composer

```
composer require whatdafox/serializer
```

Create a class that extends `Serializer\Serializer` and create a property `rules` to indicate your rules

```
<php

use Serializer\Serializer;

class AcmeSanitizer extends Serializer {

    protected $rules = [
        'name' => 'trim|strtolower|ucwords',
        'email' => 'trim|strtolower'
    ];

}
```

To use your sanitizer, just call the `sanitize()` method with the array of data like so:

```
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

That's all folks!

## Thanks

Thanks for Jeffrey Way and Laracasts for the inspiration and examples. http://laracasts.com