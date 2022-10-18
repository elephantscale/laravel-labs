# Notifications

### STEP 1) Create the Queue Job table

- Run the following command

```bash
php artisan queue:table
```

![image](https://user-images.githubusercontent.com/31894600/196491624-bd96432f-7d24-493b-92d3-ffb7e6aaeb1c.png)


```bash
php artisan migrate
```

![image](https://user-images.githubusercontent.com/31894600/196491651-2517de37-cd3a-444c-93db-0b74776dbdfa.png)


### STEP 2) Make Notifications and Listeners Queueable

In the config\queue.php file, change the default driver to use database

```php
'default' => env('QUEUE_CONNECTION', 'database'),

![image](https://user-images.githubusercontent.com/31894600/196491678-46705e46-9c88-402a-b58f-4c6742213cd5.png)
```

Change the .env file to use database as the QUEUE_CONNECTION

```php
QUEUE_CONNECTION=database
```
![image](https://user-images.githubusercontent.com/31894600/196491715-42d7c17d-c0c6-48bc-9207-24c409ac52b4.png)


implement ShouldQueue in your Notifications and Events

```php
implements ShouldQueue
```

![image](https://user-images.githubusercontent.com/31894600/196492036-e04f7dae-b50d-4ef5-9be3-ee6364cccb8a.png)

![image](https://user-images.githubusercontent.com/31894600/196492115-df1f4916-8931-4a83-a78c-7056bbf47dfb.png)


