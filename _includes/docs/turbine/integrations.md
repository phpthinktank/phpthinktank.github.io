
## Middleware integrations

### StackPHP

Basic usage with StackPHP (using `Stack\Builder` and `Stack\Run`):

```php
<?php

// index.php
<?php
require __DIR__.'/../vendor/autoload.php';

$app = new Turbine\Application();

$app->get('/', function ($request, $response) {
    $response->setContent('<h1>Hello World</h1>');
    return $response;
});

$httpKernel = new Turbine\Symfony\HttpKernelAdapter($app);

$stack = (new Stack\Builder())
    ->push('Some/MiddleWare') // This will execute first
    ->push('Some/MiddleWare') // This will execute second
    ->push('Some/MiddleWare'); // This will execute third

$app = $stack->resolve($httpKernel);
Stack\run($httpKernel); // The app will run after all the middlewares have run
```

### Zend Stratigility

Basic usage with Stratigility (using `Zend\Stratigility\MiddlewarePipe`):

```php
<?php

$application = new Application();
$application->get('/', function($request, ResponseInterface $response){
    $response->getBody()->write('Hello World');
});
$middleware = new MiddlewarePipeAdapter($application);

//wrap html heading
$middleware->pipe('/', function($request, ResponseInterface $response, $next){
    $response->getBody()->write('<h1>');

    $response = $next($request, $response);

    $response->getBody()->write('</h1>');
});

$response = $middleware(ServerRequestFactory::fromGlobals(), $application->getResponse());

echo $response->getBody(); //prints <h1>Hello World</h1>

```
