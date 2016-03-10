
## Setup

Create a new app

```php
<?php

require __DIR__.'/../vendor/autoload.php';

$app = new \Turbine\Application();
```

Create a new app with configuration

```php
<?php

$config = [
    'key' => 'value'
];
$app = new \Turbine\Application($config);
```

Add routes

```php
<?php

$app->get('/', function ($request, $response) {
    $response->getBody()->write('<h1>It works!</h1>');
    return $response;
});

$app->get('/hello/{name}', function ($request, $response, $args) {
    $response->getBody()->write(
        sprintf('<h1>Hello, %s!</h1>', $args['name'])
    );
    return $response;
});
```

Run application

```php
<?php

$app->run();
```