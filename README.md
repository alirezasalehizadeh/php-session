# PHP Session library

[![Latest Stable Version](https://poser.pugx.org/josantonius/session/v/stable)](https://packagist.org/packages/josantonius/session)
[![License](https://poser.pugx.org/josantonius/session/license)](LICENSE)
[![Total Downloads](https://poser.pugx.org/josantonius/session/downloads)](https://packagist.org/packages/josantonius/session)
[![CI](https://github.com/josantonius/php-session/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/josantonius/php-session/actions/workflows/ci.yml)
[![CodeCov](https://codecov.io/gh/josantonius/php-session/branch/master/graph/badge.svg)](https://codecov.io/gh/josantonius/php-session)
[![PSR1](https://img.shields.io/badge/PSR-1-f57046.svg)](https://www.php-fig.org/psr/psr-1/)
[![PSR4](https://img.shields.io/badge/PSR-4-9b59b6.svg)](https://www.php-fig.org/psr/psr-4/)
[![PSR12](https://img.shields.io/badge/PSR-12-1abc9c.svg)](https://www.php-fig.org/psr/psr-12/)

**Translations**: [Español](.github/lang/es-ES/README.md)

PHP library for handling sessions.

> Version 1.x is considered as deprecated and unsupported.
> In this version (2.x) the library was completely restructured.
> It is recommended to review the documentation for this version and make the necessary changes
> before starting to use it, as it not be compatible with version 1.x.

---

- [Requirements](#requirements)
- [Installation](#installation)
- [Available Methods](#available-methods)
- [Quick Start](#quick-start)
- [Usage](#usage)
- [Tests](#tests)
- [TODO](#todo)
- [Changelog](#changelog)
- [Contribution](#contribution)
- [Sponsor](#Sponsor)
- [License](#license)

---

## Requirements

This library is compatible with the PHP versions: 8.0 | 8.1.

## Installation

The preferred way to install this extension is through [Composer](http://getcomposer.org/download/).

To install **PHP Session library**, simply:

```console
composer require josantonius/session
```

The previous command will only install the necessary files,
if you prefer to **download the entire source code** you can use:

```console
composer require josantonius/session --prefer-source
```

You can also **clone the complete repository** with Git:

```console
git clone https://github.com/josantonius/php-session.git
```

## Available Methods

Available methods in this library:

### Starts the session

```php
$session->start(array $options = []): bool
```

**@see** <https://php.net/session.configuration>
for List of available `$options` and their default values.

**@throws** `SessionException` if headers already sent.

**@throws** `SessionException` if session already started.

**@throws** `SessionException` if setting options failed.

### Check if the session is started

```php
$session->isStarted(): bool
```

### Sets an attribute by name

```php
$session->set(string $name, mixed $value): void
```

**@throws** `SessionException` if session is unstarted.

### Gets an attribute by name

Optionally defines a default value when the attribute does not exist.

```php
$session->get(string $name, mixed $default = null): mixed
```

### Gets all attributes

```php
$session->all(): array
```

### Check if an attribute exists in the session

```php
$session->has(string $name);
```

### Sets several attributes at once

If attributes exist they are replaced, if they do not exist they are created.

```php
$session->replace(array $data): void
```

**@throws** `SessionException` if session is unstarted.

### Deletes an attribute by name and returns its value

Optionally defines a default value when the attribute does not exist.

```php
$session->pull(string $name, mixed $default = null): mixed
```

**@throws** `SessionException` if session is unstarted.

### Deletes an attribute by name

```php
$session->remove(string $name): void
```

**@throws** `SessionException` if session is unstarted.

### Free all session variables

```php
$session->clear(): void
```

**@throws** `SessionException` if session is unstarted.

### Gets the session ID

```php
$session->getId() string
```

### Sets the session ID

```php
$session->setId(string $sessionId): void
```

**@throws** `SessionException` if session already started.

### Update the current session id with a newly generated one

```php
$session->regenerateId(bool $deleteOldSession = false): bool
```

**@throws** `SessionException` if session is unstarted.

### Gets the session name

```php
$session->getName(): string
```

### Sets the session name

```php
$session->setName(string $name): void
```

**@throws** `SessionException` if session already started.

### Destroys the session

```php
$session->destroy(): bool
```

**@throws** `SessionException` if session is unstarted.

## Quick Start

To use this library with **Composer**:

### Using objects

```php
use Josantonius\Session\Session;

$session = new Session();
```

### Using the facade

Alternatively you can use a facade to access the methods statically:

```php
use Josantonius\Session\Facades\Session;
```

## Usage

Example of use for this library:

### - Starts the session

[Using objects](#using-objects):

Without setting options:

```php
$session->start();
```

Setting options:

```php
$session->start([
    // 'cache_expire' => 180,
    // 'cache_limiter' => 'nocache',
    // 'cookie_domain' => '',
    'cookie_httponly' => true,
    'cookie_lifetime' => 8000,
    // 'cookie_path' => '/',
    'cookie_samesite' => 'Strict',
    'cookie_secure'   => true,
    // 'gc_divisor' => 100,
    // 'gc_maxlifetime' => 1440,
    // 'gc_probability' => true,
    // 'lazy_write' => true,
    // 'name' => 'PHPSESSID',
    // 'read_and_close' => false,
    // 'referer_check' => '',
    // 'save_handler' => 'files',
    // 'save_path' => '',
    // 'serialize_handler' => 'php',
    // 'sid_bits_per_character' => 4,
    // 'sid_length' => 32,
    // 'trans_sid_hosts' => $_SERVER['HTTP_HOST'],
    // 'trans_sid_tags' => 'a=href,area=href,frame=src,form=',
    // 'use_cookies' => true,
    // 'use_only_cookies' => true,
    // 'use_strict_mode' => false,
    // 'use_trans_sid' => false,
]);
```

[Using the facade](#using-the-facade):

```php
Session::start();
```

### - Check if the session is started

[Using objects](#using-objects):

```php
$session->isStarted();
```

[Using the facade](#using-the-facade):

```php
Session::isStarted();
```

### - Sets an attribute by name

[Using objects](#using-objects):

```php
$session->set('foo', 'bar');
```

[Using the facade](#using-the-facade):

```php
Session::set('foo', 'bar');
```

### - Gets an attribute by name

[Using objects](#using-objects):

Without default value if attribute does not exist:

```php
$session->get('foo'); // null if attribute does not exist
```

With default value if attribute does not exist:

```php
$session->get('foo', false); // false if attribute does not exist
```

[Using the facade](#using-the-facade):

```php
Session::get('foo');
```

### - Gets all attributes

[Using objects](#using-objects):

```php
$session->all();
```

[Using the facade](#using-the-facade):

```php
Session::all();
```

### - Check if an attribute exists in the session

[Using objects](#using-objects):

```php
$session->has('foo');
```

[Using the facade](#using-the-facade):

```php
Session::has('foo');
```

### - Sets several attributes at once

[Using objects](#using-objects):

```php
$session->replace(['foo' => 'bar', 'bar' => 'foo']);
```

[Using the facade](#using-the-facade):

```php
Session::replace(['foo' => 'bar', 'bar' => 'foo']);
```

### - Deletes an attribute by name and returns its value

[Using objects](#using-objects):

Without default value if attribute does not exist:

```php
$session->pull('foo'); // null if attribute does not exist
```

With default value if attribute does not exist:

```php
$session->pull('foo', false); // false if attribute does not exist
```

[Using the facade](#using-the-facade):

```php
Session::pull('foo');
```

### - Deletes an attribute by name

[Using objects](#using-objects):

```php
$session->remove('foo');
```

[Using the facade](#using-the-facade):

```php
Session::remove('foo');
```

### - Free all session variables

[Using objects](#using-objects):

```php
$session->clear();
```

[Using the facade](#using-the-facade):

```php
Session::clear();
```

### - Gets the session ID

[Using objects](#using-objects):

```php
$session->getId();
```

[Using the facade](#using-the-facade):

```php
Session::getId();
```

### - Sets the session ID

[Using objects](#using-objects):

```php
$session->setId('foo');
```

[Using the facade](#using-the-facade):

```php
Session::setId('foo');
```

### - Update the current session id with a newly generated one

[Using objects](#using-objects):

Regenerate ID without deleting the old session:

```php
$session->regenerateId();
```

Regenerate ID by deleting the old session:

```php
$session->regenerateId(true);
```

[Using the facade](#using-the-facade):

```php
Session::regenerateId();
```

### - Gets the session name

[Using objects](#using-objects):

```php
$session->getName();
```

[Using the facade](#using-the-facade):

```php
Session::getName();
```

### - Sets the session name

[Using objects](#using-objects):

```php
$session->setName('foo');
```

[Using the facade](#using-the-facade):

```php
Session::setName('foo');
```

### - Destroys the session

[Using objects](#using-objects):

```php
$session->destroy();
```

[Using the facade](#using-the-facade):

```php
Session::destroy();
```

## Tests

To run [tests](tests) you just need [composer](http://getcomposer.org/download/) and to execute the following:

```console
git clone https://github.com/josantonius/php-session.git
```

```console
cd php-session
```

```console
composer install
```

Run unit tests with [PHPUnit](https://phpunit.de/):

```console
composer phpunit
```

Run code standard tests with [PHPCS](https://github.com/squizlabs/PHP_CodeSniffer):

```console
composer phpcs
```

Run [PHP Mess Detector](https://phpmd.org/) tests to detect inconsistencies in code style:

```console
composer phpmd
```

Run all previous tests:

```console
composer tests
```

## TODO

- [ ] Add new feature
- [ ] Improve tests
- [ ] Improve documentation
- [ ] Improve English translation in the README file
- [ ] Refactor code for disabled code style rules (see phpmd.xml and phpcs.xml)
- [ ] Show an example of renewing the session lifetime
- [ ] Feature to enable/disable exceptions?
- [ ] Feature to add prefixes in session attributes?

## Changelog

Detailed changes for each release are documented in the
[release notes](https://github.com/josantonius/php-session/releases).

## Contribution

Please make sure to read the [Contributing Guide](.github/CONTRIBUTING.md), before making a pull
request, start a discussion or report a issue.

Thanks to all [contributors](https://github.com/josantonius/php-session/graphs/contributors)! :heart:

## Sponsor

If this project helps you to reduce your development time,
[you can sponsor me](https://github.com/josantonius#sponsor) to support my open source work :blush:

## License

This repository is licensed under the [MIT License](LICENSE).

Copyright © 2017-present, [Josantonius](https://github.com/josantonius#contact)
