
## Configuration

Extend configuration of an existing instance

```php
<?php

//add many values
$app->setConfig([
    'database' => 'mysql://root:root@localhost/acmedb',
    'services' => [
        'Acme\Services\ViewProvider',
    ]
]);

//add a single value
$app->setConfig('baseurl' => 'localhost/');
```

Access configuration

```php
<?php

//access all configuration
$app->getConfig();

//get one configuration item
$app->getConfig('database');
```
