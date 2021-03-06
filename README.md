# ContainerDI

Simple IoC container with some method: bind, singleton, resolve, make.

## Install

### Install Composer
```bash
composer require iquxbyte/container-di
```

### Install Non-Composer
Just download this repo and include `path/to/src/__autoload.php`.

## Use

### Bind

```php
ContainerDI::bind(Foo::class);
```

### Singleton

```php
ContainerDI::singleton(FooBarContract::class, FooBar::class);
```

### Make class

```php
ContainerDI::make(FooBarContract::class, FooBar::class);
```

### Resolve class

```php
ContainerDI::make(Foo::class);
```

## Example

```php
<?php

use IquxByte\ContainerDI;

require_once '../src/__autoload.php';
require_once 'class.php';

/**
 * Simple bind class to container
 */
ContainerDI::bind(Foo::class);

/**
 * bind with custom name
 */
ContainerDI::bind('class.foo', Foo::class);

/**
 * use closure to bind
 */
ContainerDI::bind(Foo::class, function ($containerDI) {
    return new Foo;
});

/**
 * bind class with interface to container
 */
ContainerDI::bind(FooBarContract::class, FooBar::class);

/**
 * Get instance
 */
$instance = ContainerDI::make(FooBar::class);

/**
 * Get class from interface
 */
$instance = ContainerDI::make(FooBarContract::class);

/**
 * Singleton class to container
 */
ContainerDI::singleton(Bar::class);

/**
 * Test singleton
 * should be true
 */
var_dump(ContainerDI::make(Bar::class) === ContainerDI::make(Bar::class));

/**
 * Test bind
 * should be false
 */
var_dump(ContainerDI::make(FooBarContract::class) === ContainerDI::make(FooBarContract::class));
```