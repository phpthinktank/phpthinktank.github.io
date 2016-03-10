
## Dependency Injection Container

Turbine uses `League/Container` as its dependency injection container.

You can bind singleton objects into the container from the main application object using ArrayAccess:

```php
<?php

$app['db'] = function () {
    $manager = new Illuminate\Database\Capsule\Manager;

    $manager->addConnection([
        'driver'    => 'mysql',
        'host'      => $config['db_host'],
        'database'  => $config['db_name'],
        'username'  => $config['db_user'],
        'password'  => $config['db_pass'],
        'charset'   => 'utf8',
        'collation' => 'utf8_unicode_ci'
    ], 'default');

    $manager->setAsGlobal();

    return $manager;
};
```

or by accessing the container directly:

```php
<?php

$app->getContainer()->share('db', function () {
    $manager = new Illuminate\Database\Capsule\Manager;

    $manager->addConnection([
        'driver'    => 'mysql',
        'host'      => $config['db_host'],
        'database'  => $config['db_name'],
        'username'  => $config['db_user'],
        'password'  => $config['db_pass'],
        'charset'   => 'utf8',
        'collation' => 'utf8_unicode_ci'
    ], 'default');

    $manager->setAsGlobal();

    return $manager;
});
```

Multitons can be added using the `add` method on the container:

```php
<?php

//callback
$app->getContainer()->add('foo', function () {
    return new Foo();
});
```

For more information about `league/container` check out this page - [http://container.thephpleague.com/](http://container.thephpleague.com/).

### Service providers

Service providers can be registered using the `register` method on the Turbine app or `addServiceProvider` on the container:

```php
<?php

$app->register('\My\Service\Provider');
$app->getContainer()->addServiceProvider('\My\Service\Provider');
```

For more information about service providers check out this page - [http://container.thephpleague.com/service-providers/](http://container.thephpleague.com/service-providers/).

### Custom container

Set your own container (needs an instance of `\League\Container\ContainerInterface`)

```php
<?php

$app->setContainer($container);
```

Get container

```php
<?php

$app->getContainer();
```
