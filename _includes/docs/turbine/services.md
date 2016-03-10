
## Services

Turbine uses dependecy injection container to access it's services. Following integrations can be exchanged.

### Configurator

Uses in `Application::setConfig()`,`Application::getConfig()` and `Application::hasConfig()`

```php
<?php

$app->getConfigurator();
``` 

```php
<?php

$app->getContainer()->share(\ArrayAccess::class, \ArrayObject::class)
```

### error handler

```php
<?php

$app->getContainer()->share(\Whoops\Run::class, new \Whoops\Run());
```

```php
<?php

$app->getErrorHandler()
``` 

### error response handler

```php
<?php

$app->getContainer()->share(\Whoops\Handler\HandlerInterface::class, Acme\ErrorResponseHandler::class);
```

```php
<?php

$app->getErrorResponseHandler()
``` 

### psr logger

Get a new logger instance by channel name

```php
<?php

$app->getContainer()->add(\Psr\Log\LoggerInterface::class, \Monolog\Logger::class);
```

```php
<?php

$app->getLogger('channel name');
``` 

### psr server request

```php
<?php

$app->getContainer()->share(\Psr\Http\Message\ServerRequestInterface::class, \Zend\Diactoros\ServerRequestFactory::fromGlobals());
```

```php
<?php

$app->getRequest()
``` 

### psr response

```php
<?php

$app->getContainer()->add(\Psr\Http\Message\ResponseInterface::class, \Zend\Diactoros\Response::class);
```

```php
<?php

$app->getRequest()
``` 

### response emitter

```php
<?php

$app->getContainer()->share(\Zend\Diactoros\Response\EmitterInterface::class, \Zend\Diactoros\Response\SapiEmitter::class);
```

```php
<?php

$app->getResponseEmitter()
``` 
