logPHPMailer
================

[![Latest Stable Version][icon-stable-version]][link-packagist]
[![Latest Untable Version][icon-unstable-version]][link-packagist]
[![Total Downloads][icon-downloads]][link-packagist]
[![License][icon-license]][link-license]
[![PHP][icon-php]][link-php]

[![Linux Build Status][icon-travis]][link-travis]
[![Windows Build Status][icon-appveyor]][link-appveyor]
[![Code Coverage][icon-coverage]][link-coverage]
[![Code Quality][icon-quality]][link-quality]

logPHPMailer is a [PHPMailer][link-phpmailer] handler for [Log][link-log]. It enables you to send logs to emails with PHPMailer.

## Installation

### Requirements

logPHPMailer requires *[PHP][link-php] 5.5.0* or higher, *[Log][link-log] 1.x or 2.x* and *[PHPMailer][link-phpmailer] 6.x*.

### Using Composer

The reccomended way to install logPHPMailer is with [Composer][link-composer], dependency manager for PHP.

You should just add `PeteKip/log-phpmailer` to your project dependencies in `composer.json`. It will also install Log and PHPMailer, but it is reccomended to add them manually to `composer.json`.

```json
{
    "require": {
        "log/log": "^1.0",
        "phpmailer/phpmailer": "^6.0",
        "petekip/log-phpmailer": "^1.0"
    }
}
```

Do not forget to run `composer install` and add `require 'vendor/autoload.php';` to your main script.

### Manually Installation

Alternatively, you could download all files in directory [`src`][link-handlers] from GitHub and then manually include them in your script. You also have to install Log and PHPMailer manually.

## Usage

You should just add handler `logPHPMailer\PHPMailerHandler` to your logger. It's first argument must be PHPMailer instance.

## Example

```php
<?php

use logPHPMailer\PHPMailerHandler;

use Log\Formatter\HtmlFormatter;
use Log\Logger;
use Log\Processor\IntrospectionProcessor;
use Log\Processor\MemoryUsageProcessor;
use Log\Processor\WebProcessor;

use PHPMailer\PHPMailer\PHPMailer;

require __DIR__ . '/vendor/autoload.php';

$mailer = new PHPMailer(true);
$logger = new Logger('logger');

$mailer->isSMTP();
$mailer->Host = 'smtp.example.com';
$mailer->SMTPAuth = true;
$mailer->Username = 'server@example.com';
$mailer->Password = 'password';

$mailer->setFrom('server@example.com', 'Logging Server');
$mailer->addAddress('user@example.com', 'Your Name');

$logger->pushProcessor(new IntrospectionProcessor);
$logger->pushProcessor(new MemoryUsageProcessor);
$logger->pushProcessor(new WebProcessor);

$handler = new PHPMailerHandler($mailer);
$handler->setFormatter(new HtmlFormatter);

$logger->pushHandler($handler);

$logger->error('Error!');
$logger->alert('Something went wrong!');

```

## Versioning
This library uses [SemVer][link-semver] SemVer for versioning. For the versions available, see the [tags on this repository][link-tags].

## License
This library is licensed under the MIT license. See the [LICENSE][link-license-file] file for details.

[icon-stable-version]: https://img.shields.io/packagist/v/PeteKip/log-phpmailer.svg?style=flat-square&label=Latest+Stable+Version
[icon-unstable-version]: https://img.shields.io/packagist/vpre/PeteKip/log-phpmailer.svg?style=flat-square&label=Latest+Unstable+Version
[icon-downloads]: https://img.shields.io/packagist/dt/PeteKip/log-phpmailer.svg?style=flat-square&label=Downloads
[icon-license]: https://img.shields.io/packagist/l/PeteKip/log-phpmailer.svg?style=flat-square&label=License
[icon-php]: https://img.shields.io/packagist/php-v/PeteKip/log-phpmailer.svg?style=flat-square&label=PHP
[icon-travis]: https://img.shields.io/travis/com/PeteKip/logPHPMailer.svg?style=flat-square&label=Linux+Build+Status
[icon-appveyor]: https://img.shields.io/appveyor/ci/PeteKip/logPHPMailer.svg?style=flat-square&label=Windows+Build+Status
[icon-coverage]: https://img.shields.io/scrutinizer/coverage/g/PeteKip/logPHPMailer.svg?style=flat-square&label=Code+Coverage
[icon-quality]: https://img.shields.io/scrutinizer/g/PeteKip/logPHPMailer.svg?style=flat-square&label=Code+Quality

[link-packagist]: https://packagist.org/packages/PeteKip/log-phpmailer/
[link-license]: https://choosealicense.com/licenses/mit/
[link-php]: https://php.net/
[link-travis]: https://travis-ci.com/PeteKip/logPHPMailer/
[link-appveyor]: https://ci.appveyor.com/project/PeteKip/logphpmailer/
[link-coverage]: https://scrutinizer-ci.com/g/PeteKip/logPHPMailer/code-structure/
[link-quality]: https://scrutinizer-ci.com/g/PeteKip/logPHPMailer/

[link-log]: https://github.com/Seldaek/log/
[link-phpmailer]: https://github.com/PHPMailer/PHPMailer/
[link-composer]: https://getcomposer.org/
[link-handlers]: https://github.com/PeteKip/logPHPMailer/tree/master/src
[link-semver]: https://semver.org/
[link-tags]: https://github.com/PeteKip/logPHPMailer/tags/
[link-license-file]: https://github.com/PeteKip/logPHPMailer/blob/master/LICENSE
# logPHPMailer
