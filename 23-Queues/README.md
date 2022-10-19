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

### STEP 3) Install Supervisor

Run the following command

```bash
sudo apt-get install supervisor
```

Navigate to Supervisor configuration folder
```bash
cd /etc/supervisor/conf.d
```

Create a new worker configuration file
```bash
sudo nano laraver-worker.conf 
```

Add the following code to the file

```bash
[program:laravel-worker]
process_name=%(program_name)s_%(process_num)02d
command=php /home/ubuntu/course/artisan queue:work --sleep=3 --tries=3 
autostart=true
autorestart=true
user=ubuntu
stdout_logfile=/home/ubuntu/course/worker.log

```

Run the following command
```bash
sudo supervisorctl reread
```
```bash
sudo supervisorctl update
```
```bash
sudo supervisorctl start laravel-worker:*
```



