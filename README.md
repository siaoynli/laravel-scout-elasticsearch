# Laravel Scout Elasticsearch Driver

## Installation

You can install the package via composer:

```bash
composer require siaoynli/laravel-scout-elasticsearch
```

You must add the Scout service provider and the package service provider in your app.php config:

```php
// config/app.php
'providers' => [
    ...
    Laravel\Scout\ScoutServiceProvider::class,
    ...
    Siaoynli\ScoutEngines\Elasticsearch\ElasticsearchProvider::class,
],
```

### Setting up Elasticsearch configuration

```php
// config/scout.php
// Set your driver to elasticsearch
    'driver' => env('SCOUT_DRIVER', 'elasticsearch'),

...
    'elasticsearch' => [
        'index' => env('ELASTICSEARCH_INDEX', 'laravel'),
        'hosts' => [
            env('ELASTICSEARCH_HOST', 'http://localhost'),
        ],
    ],
...
```

## License

The MIT License (MIT).
