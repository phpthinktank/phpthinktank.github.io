
## Debugging

Turbine provides advanced error handling and logging.

### Error handling

Turbine is using Whoops error handling framework and determines the error handler by request content type.

Set your own handler:

```php
<?php

$app->getErrorHandler()->push(new Acme\ErrorResponseHandler);
```

For more information about handlers read this guide - 

By default Turbine runs with error options disabled. To enable debugging add

```php
<?php

$app->setConfig('error', true);
```

By default Turbine is catching all errors. To disable error catching add

```php
<?php

$app->setConfig('error.catch', false);
```

### Logging

Turbine has built in support for Monolog. To access a channel call:

```php
<?php

$app->getLogger('channel name');
```

For more information about channels read this guide - [https://github.com/Seldaek/monolog/blob/master/doc/usage.md#leveraging-channels](https://github.com/Seldaek/monolog/blob/master/doc/usage.md#leveraging-channels).

