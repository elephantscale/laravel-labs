# Notifications

### STEP 1) Create the Queue Job table

- Run the following command

```bash
php artisan queue:table
```

```bash
php artisan migrate
```

### STEP 2) Make Notifications Queueable

In the config\queue.php file, change the default driver to use database

```php
'default' => env('QUEUE_CONNECTION', 'database'),
```

Change the .env file to use database as the QUEUE_CONNECTION

```php
QUEUE_CONNECTION=database
```



