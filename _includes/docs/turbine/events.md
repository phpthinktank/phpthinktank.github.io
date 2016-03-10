
## Events

You can intercept requests and responses at three points during the lifecycle:

### request.received

```php
<?php

$app->subscribe($app::EVENT_REQUEST_RECEIVED, function ($event, $request) {
    // manipulate request
});
```

This event is fired when a request is received but before it has been processed by the router.

### response.created

```php
<?php

$app->subscribe($app::EVENT_RESPONSE_CREATED, function ($event, $request, $response) {
    //manipulate request or response
});
```

This event is fired when a response has been created but before it has been output.

### response.sent

```php
<?php

$app->subscribe($app::EVENT_RESPONSE_SENT, function ($event, $request, $response) {
    //manipulate request and response
});
```

This event is fired when a response has been output and before the application lifecycle is completed.

### runtime.error

```php
<?php

$app->subscribe($app::EVENT_RUNTIME_ERROR, function ($event, $exception) use ($app) {
    //process exception
});
```

This event is always fired when an error occurs.

### lifecycle.error

`$errorResponse` is used as default response

```php
<?php

$app->subscribe($app::EVENT_LIFECYCLE_ERROR, function ($event, $exception, $errorResponse, $request, $response) {
    //manipulate $errorResponse and process exception
});
```

This event is fired only when an error occurs while handling request/response lifecycle. 
This event is fired after runtime.error

### lifecycle.complete

```php
<?php

$app->subscribe($app::EVENT_LIFECYCLE_COMPLETE, function ($event, $request, $response) {
    // access the request using $event->getRequest()
    // access the response using $event->getResponse()
})
```

This event is fired when a response has been output and before the application lifecycle is completed.

### Custom Events

You can fire custom events using the event emitter directly:

```php
<?php

// Subscribe
$app->subscribe('custom.event', function ($event, $time) {
    return 'the time is '.$time;
});

// Publish
$app->getEventEmitter()->emit('custom.event', time());
```