# Laravel Reportable

[![Build Status](https://img.shields.io/travis/faustbrian/Laravel-Reportable/master.svg?style=flat-square)](https://travis-ci.org/faustbrian/Laravel-Reportable)
[![PHP from Packagist](https://img.shields.io/packagist/php-v/faustbrian/laravel-reportable.svg?style=flat-square)]()
[![Latest Version](https://img.shields.io/github/release/faustbrian/Laravel-Reportable.svg?style=flat-square)](https://github.com/faustbrian/Laravel-Reportable/releases)
[![License](https://img.shields.io/packagist/l/faustbrian/Laravel-Reportable.svg?style=flat-square)](https://packagist.org/packages/faustbrian/Laravel-Reportable)

## Installation

Require this package, with [Composer](https://getcomposer.org/), in the root directory of your project.

``` bash
$ composer require faustbrian/laravel-reportable
```

To get started, you'll need to publish the vendor assets and migrate:

```
php artisan vendor:publish --provider="BrianFaust\Reportable\ReportableServiceProvider" && php artisan migrate
```

## Usage

## Setup a Model
``` php
<?php

namespace App;

use BrianFaust\Reportable\HasReports;
use Illuminate\Database\Eloquent\Model;

class Post extends Model
{
    use HasReports;
}
```

## Examples

#### The User Model reports the Post Model
``` php
$post->report([
    'reason' => \Str::random(10),
    'meta' => ['some more optional data, can be notes or something'],
], $user);
```

#### Create a conclusion for a Report and add the User Model as "judge" (useful to later see who or what came to this conclusion)
``` php
$report->conclude([
    'conclusion' => 'Your report was valid. Thanks! We\'ve taken action and removed the entry.',
    'action_taken' => 'Record has been deleted.' // This is optional but can be useful to see what happend to the record
    'meta' => ['some more optional data, can be notes or something'],
], $user);
```

#### Get the conclusion for the Report Model
``` php
$report->conclusion;
```

#### Get the judge for the Report Model (only available if there is a conclusion)
``` php
$report->judge(); // Just a shortcut for $report->conclusion->judge
```

#### Get an array with all Judges that have ever "judged" something
``` php
Report::allJudges();
```

## Testing

``` bash
$ phpunit
```

## Security

If you discover a security vulnerability within this package, please send an e-mail to hello@brianfaust.me. All security vulnerabilities will be promptly addressed.

## Credits

- [Brian Faust](https://github.com/faustbrian)
- [All Contributors](../../contributors)

## License

[MIT](LICENSE) © [Brian Faust](https://brianfaust.me)
