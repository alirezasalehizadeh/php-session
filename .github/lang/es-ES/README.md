# PHP Session library

[![Latest Stable Version](https://poser.pugx.org/josantonius/session/v/stable)](https://packagist.org/packages/josantonius/session)
[![License](https://poser.pugx.org/josantonius/session/license)](LICENSE)
[![Total Downloads](https://poser.pugx.org/josantonius/session/downloads)](https://packagist.org/packages/josantonius/session)
[![CI](https://github.com/josantonius/php-session/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/josantonius/php-session/actions/workflows/ci.yml)
[![CodeCov](https://codecov.io/gh/josantonius/php-session/branch/master/graph/badge.svg)](https://codecov.io/gh/josantonius/php-session)
[![PSR1](https://img.shields.io/badge/PSR-1-f57046.svg)](https://www.php-fig.org/psr/psr-1/)
[![PSR4](https://img.shields.io/badge/PSR-4-9b59b6.svg)](https://www.php-fig.org/psr/psr-4/)
[![PSR12](https://img.shields.io/badge/PSR-12-1abc9c.svg)](https://www.php-fig.org/psr/psr-12/)

**Traducciones**: [English](/README.md)

Biblioteca PHP para manejo de sesiones.

> La versión 1.x se considera obsoleta y sin soporte.
> En esta versión (2.x) la biblioteca fue completamente reestructurada.
> Se recomienda revisar la documentación de esta versión y hacer los cambios necesarios
> antes de empezar a utilizarla, ya que no es compatible con la versión 1.x.

---

- [Requisitos](#requisitos)
- [Instalación](#instalación)
- [Métodos disponibles](#métodos-disponibles)
- [Cómo empezar](#cómo-empezar)
- [Uso](#uso)
- [Tests](#tests)
- [Tareas pendientes](#tareas-pendientes)
- [Registro de Cambios](#registro-de-cambios)
- [Contribuir](#contribuir)
- [Patrocinar](#patrocinar)
- [Licencia](#licencia)

---

## Requisitos

Esta biblioteca es compatible con las versiones de PHP: 8.0 | 8.1.

## Instalación

La mejor forma de instalar esta extensión es a través de [Composer](http://getcomposer.org/download/).

Para instalar **PHP Session library**, simplemente escribe:

```console
composer require josantonius/session
```

El comando anterior sólo instalará los archivos necesarios,
si prefieres **descargar todo el código fuente** puedes utilizar:

```console
composer require josantonius/session --prefer-source
```

También puedes **clonar el repositorio** completo con Git:

```console
git clone https://github.com/josantonius/php-session.git
```

## Métodos disponibles

Métodos disponibles en esta biblioteca:

### Iniciar la sesión

```php
$session->start(array $options = []): bool
```

**@see** <https://php.net/session.configuration>
para ver la lista de las `$opciones` disponibles y sus valores por defecto.

**@throws** `SessionException` si los _headers_ ya se enviaron.

**@throws** `SessionException` si la sesión ya está iniciada.

**@throws** `SessionException` si hay algún fallo con las opciones.

### Comprobar si la sesión está iniciada

```php
$session->isStarted(): bool
```

### Establecer un atributo por su nombre

```php
$session->set(string $name, mixed $value): void
```

**@throws** `SessionException` si la sesión no está iniciada.

### Obtener un atributo por su nombre

Opcionalmente define un valor por defecto cuando el atributo no existe.

```php
$session->get(string $name, mixed $default = null): mixed
```

### Obtener todos los atributos

```php
$session->all(): array
```

### Comprobar si un atributo existe en la sesión

```php
$session->has(string $name): bool
```

### Establecer múltiples atributos de una vez

Si los atributos existen se sustituyen, si no existen se crean.

```php
$session->replace(array $data): void
```

**@throws** `SessionException` si la sesión no está iniciada.

### Eliminar un atributo por su nombre y devolver su valor

Opcionalmente define un valor por defecto cuando el atributo no existe.

```php
$session->pull(string $name, mixed $default = null): mixed
```

**@throws** `SessionException` si la sesión no está iniciada.

### Eliminar un atributo por su nombre

```php
$session->remove(string $name): void
```

**@throws** `SessionException` si la sesión no está iniciada.

### Liberar todas las variables de la sesión

```php
$session->clear(): void
```

**@throws** `SessionException` si la sesión no está iniciada.

### Obtiene el ID de la sesión

```php
$session->getId(): string
```

### Establecer el ID de la sesión

```php
$session->setId(string $sessionId): void
```

**@throws** `SessionException` si la sesión ya está iniciada.

### Actualizar el ID de la sesión actual con uno recién generado

```php
$session->regenerateId(bool $deleteOldSession = false): bool
```

**@throws** `SessionException` si la sesión no está iniciada.

### Obtener el nombre de la sesión

```php
$session->getName(): string
```

### Establecer el nombre de la sesión

```php
$session->setName(string $name): void
```

**@throws** `SessionException` si la sesión ya está iniciada.

### Eliminar la sesión

```php
$session->destroy(): bool
```

**@throws** `SessionException` si la sesión no está iniciada.

## Cómo empezar

### Utilizando objetos

```php
use Josantonius\Session\Session;

$session = new Session();
```

### Utilizando la fachada

Alternativamente puedes utilizar la fachada para acceder a los métodos de manera estática:

```php
use Josantonius\Session\Facades\Session;
```

## Uso

Ejemplo de uso para esta biblioteca:

### - Iniciar la sesión

[Utilizando objetos](#utilizando-objetos):

Sin establecer opciones:

```php
$session->start();
```

Estableciendo opciones:

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

[Utilizando la fachada](#utilizando-la-fachada):

```php
Session::start();
```

### - Comprobar si la sesión está iniciada

[Utilizando objetos](#utilizando-objetos):

```php
$session->isStarted();
```

[Utilizando la fachada](#utilizando-la-fachada):

```php
Session::isStarted();
```

### - Establecer un atributo por su nombre

[Utilizando objetos](#utilizando-objetos):

```php
$session->set('foo', 'bar');
```

[Utilizando la fachada](#utilizando-la-fachada):

```php
Session::set('foo', 'bar');
```

### - Obtener un atributo por su nombre

[Utilizando objetos](#utilizando-objetos):

Sin valor por defecto si el atributo no existe:

```php
$session->get('foo'); // null si el atributo no existe
```

Con valor por defecto si el atributo no existe:

```php
$session->get('foo', false); // false si el atributo no existe
```

[Utilizando la fachada](#utilizando-la-fachada):

```php
Session::get('foo');
```

### - Obtener todos los atributos

[Utilizando objetos](#utilizando-objetos):

```php
$session->all();
```

[Utilizando la fachada](#utilizando-la-fachada):

```php
Session::all();
```

### - Comprobar si un atributo existe en la sesión

[Utilizando objetos](#utilizando-objetos):

```php
$session->has('foo');
```

[Utilizando la fachada](#utilizando-la-fachada):

```php
Session::has('foo');
```

### - Establecer múltiples atributos de una vez

[Utilizando objetos](#utilizando-objetos):

```php
$session->replace(['foo' => 'bar', 'bar' => 'foo']);
```

[Utilizando la fachada](#utilizando-la-fachada):

```php
Session::replace(['foo' => 'bar', 'bar' => 'foo']);
```

### - Eliminar un atributo por su nombre y devolver su valor

[Utilizando objetos](#utilizando-objetos):

Sin valor por defecto si el atributo no existe:

```php
$session->pull('foo'); // null si el atributo no existe
```

Con valor por defecto si el atributo no existe:

```php
$session->pull('foo', false); // false si el atributo no existe
```

[Utilizando la fachada](#utilizando-la-fachada):

```php
Session::pull('foo');
```

### - Eliminar un atributo por su nombre

[Utilizando objetos](#utilizando-objetos):

```php
$session->remove('foo');
```

[Utilizando la fachada](#utilizando-la-fachada):

```php
Session::remove('foo');
```

### - Liberar todas las variables de la sesión

[Utilizando objetos](#utilizando-objetos):

```php
$session->clear();
```

[Utilizando la fachada](#utilizando-la-fachada):

```php
Session::clear();
```

### - Obtiene el ID de la sesión

[Utilizando objetos](#utilizando-objetos):

```php
$session->getId();
```

[Utilizando la fachada](#utilizando-la-fachada):

```php
Session::getId();
```

### - Establecer el ID de la sesión

[Utilizando objetos](#utilizando-objetos):

```php
$session->setId('foo');
```

[Utilizando la fachada](#utilizando-la-fachada):

```php
Session::setId('foo');
```

### - Actualizar el ID de la sesión actual con uno recién generado

[Utilizando objetos](#utilizando-objetos):

Regenerar el ID sin borrar la sesión anterior:

```php
$session->regenerateId();
```

Regenerar el ID borrando la sesión anterior:

```php
$session->regenerateId(true);
```

[Utilizando la fachada](#utilizando-la-fachada):

```php
Session::regenerateId();
```

### - Obtener el nombre de la sesión

[Utilizando objetos](#utilizando-objetos):

```php
$session->getName();
```

[Utilizando la fachada](#utilizando-la-fachada):

```php
Session::getName();
```

### - Establecer el nombre de la sesión

[Utilizando objetos](#utilizando-objetos):

```php
$session->setName('foo');
```

[Utilizando la fachada](#utilizando-la-fachada):

```php
Session::setName('foo');
```

### - Eliminar la sesión

[Utilizando objetos](#utilizando-objetos):

```php
$session->destroy();
```

[Utilizando la fachada](#utilizando-la-fachada):

```php
Session::destroy();
```

## Tests

Para ejecutar las [pruebas](tests) necesitarás [Composer](http://getcomposer.org/download/) y seguir los siguientes pasos:

```console
git clone https://github.com/josantonius/php-session.git
```

```console
cd php-session
```

```console
composer install
```

Ejecutar pruebas unitarias con [PHPUnit](https://phpunit.de/):

```console
composer phpunit
```

Ejecutar pruebas de estándares de código con [PHPCS](https://github.com/squizlabs/PHP_CodeSniffer):

```console
composer phpcs
```

Ejecutar pruebas con [PHP Mess Detector](https://phpmd.org/) para detectar inconsistencias en el estilo de codificación:

```console
composer phpmd
```

Ejecutar todas las pruebas anteriores:

```console
composer tests
```

## Tareas pendientes

- [ ] Añadir nueva funcionalidad
- [ ] Mejorar pruebas
- [ ] Mejorar documentación
- [ ] Mejorar la traducción al inglés en el archivo README
- [ ] Refactorizar código para las reglas de estilo de código deshabilitadas
(ver [phpmd.xml](phpmd.xml) y [phpcs.xml](phpcs.xml))
- [ ] Mostrar un ejemplo de renovación de la duración de la sesión
- [ ] ¿Funcionalidad para activar/desactivar excepciones?
- [ ] ¿Funcionalidad para añadir prefijos en los atributos de sesión?

## Registro de Cambios

Los cambios detallados de cada versión se documentan en las
[notas de la misma](https://github.com/josantonius/php-session/releases).

## Contribuir

Por favor, asegúrate de leer la [Guía de contribución](CONTRIBUTING.md) antes de hacer un
_pull request_, comenzar una discusión o reportar un _issue_.

¡Gracias por [colaborar](https://github.com/josantonius/php-session/graphs/contributors)! :heart:

## Patrocinar

Si este proyecto te ayuda a reducir el tiempo de desarrollo,
[puedes patrocinarme](https://github.com/josantonius/lang/es-ES/README.md#patrocinar)
para apoyar mi trabajo :blush:

## Licencia

Este repositorio tiene una licencia [MIT License](LICENSE).

Copyright © 2017-actualidad, [Josantonius](https://github.com/josantonius/lang/es-ES/README.md#contacto)
