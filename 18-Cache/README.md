# Implement Cache

### STEP 1) Install Clockwork tool (Not mandatory but a nice to have)

- Install the Clockwork extension

https://addons.mozilla.org/en-US/firefox/addon/clockwork-dev-tools/

- Run the following command
```bash
  composer require itsgoingd/clockwork
```

Once Installed please ask the trainer to do quick overview and explain how it works.


### STEP 2) Add Cache to get the Movies function

In the `MoviesController.php` replace the Indec function with the following code.

```php
 public function index()
 {
    return MoviesResource::collection(Cache::remember('movies',  60, function()
    {
        return Movie::all();
    }));
 }
```

### STEP 3) Add an Observer

Run the following command to create a new Observer

```bash
php artisan make:observer MoviesObserver --model=Movie
```

### STEP 4) Link the new Observer to the Movie Model

Add the follwing code in the boot() function in the `AppServiceProvider.php`

```php
Movie::observe(classes: MoviesObserver::class);
```

### STEP 5) Clean cache when a new Movie es created

Add the following line in the Created() function on the`MoviesObserver.php`

```php
Cache::forget('movies');
```

### STEP 6) Install Redis

Run the following command

```bash
sudo apt update
```
```bash
sudo apt install redis-server
```
```bash
composer require predis/predis
```

### STEP 7) Configure Redis as your Cache driver

In the file `config/database.php`, replace the `redis` section 

```bash
'redis' => [

        'client' => env('REDIS_CLIENT', 'predis'),

        'options' => [
            'cluster' => env('REDIS_CLUSTER', 'redis'),
            'prefix' => env('REDIS_PREFIX', Str::slug(env('APP_NAME', 'laravel'), '_').'_database_'),
        ],

        'default' => [
            'url' => env('REDIS_URL'),
            'host' => env('REDIS_HOST', '127.0.0.1'),
            'password' => env('REDIS_PASSWORD', null),
            'port' => env('REDIS_PORT', '6379'),
            'database' => env('REDIS_DB', '0'),
        ],

        'cache' => [
            'url' => env('REDIS_URL'),
            'host' => env('REDIS_HOST', '127.0.0.1'),
            'password' => env('REDIS_PASSWORD', null),
            'port' => env('REDIS_PORT', '6379'),
            'database' => env('REDIS_CACHE_DB', '1'),
        ],

    ]
```

In the file `config/cache.php`, change the default driver to redis

```bash
'default' => env('CACHE_DRIVER', 'redis'),
```

In the `.env` file add 

```bash
REDIS_CLIENT=predis
```

In the `.env` change the`CACHE-DRIVER` to `redis`

```bash
CACHE_DRIVER=redis
```

