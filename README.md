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

## 说明

包依赖 elasticsearch/elasticsearch
安装 elasticsearch/elasticsearch 包如果>=7.4 需要修改
Elasticsearch\Endpoints\Search
删除 26 行，否则会报错

```
if (isset($type)) {
            trigger_error('Specifying types in urls has been deprecated', E_USER_DEPRECATED);
}
```

如果需要排序功能
修改 Laravel\Scout\Searchable
getScoutModelsByIds 函数 增加排序功能,并且排序字段定义的时候需要和表字段相同

```
         $query = $query->whereIn(
             $this->getScoutKeyName(),
             $ids
         );

         //排序
         if (count($builder->orders)) {
             foreach ($builder->orders as  $order) {
                 $query = $query->orderBy($order["column"], $order["direction"]);
             }
         }
         return $query->get();
```

## License

The MIT License (MIT).
