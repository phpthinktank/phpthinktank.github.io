
## Routing

Basic usage with anonymous functions:

```php
<?php

// index.php
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

$app->run();
```

Basic usage with controllers:

```php
<?php

// index.php
<?php

require __DIR__.'/../vendor/autoload.php';

$app = new Turbine\Application();

$app->get('/', 'HomeController::index'); // calls index method on HomeController class

$app->run();
```

```php
<?php

// HomeController.php
<?php

use Psr\Http\Message\ServerRequestInterface;
use Psr\Http\Message\ResponseInterface;

class HomeController
{
    public function index(ServerRequestInterface $request, ResponseInterface $response, array $args)
    {
        $response->getBody()->write('<h1>It works!</h1>');
        return $response;
    }
}
```

Automatic constructor injection of controllers:

```php
<?php

// index.php
<?php

require __DIR__.'/../vendor/autoload.php';

$app = new Turbine\Application();

$app->share('App\CustomService', new App\CustomService)
$app->get('/', 'HomeController::index'); // calls index method on HomeController class

$app->run();
```

```php
<?php

// HomeController.php
<?php

use Psr\Http\Message\ServerRequestInterface;
use Psr\Http\Message\ResponseInterface;

class HomeController
{
    /**
     * @var App\CustomService
     */
    private $service;

    /**
     * @param App\CustomService $application
     */
    public function __construct(App\CustomService $service = null)
    {
        $this->service = $service;
    }

    /**
     * @return App\CustomService
     */
    public function getService()
    {
        return $this->service;
    }
    
    public function index(ServerRequestInterface $request, ResponseInterface $response, array $args)
    {
        //do somehing with service
        $service = $this->getService();
    
        $response->getBody()->write();
        return $response;
    }
}
```
