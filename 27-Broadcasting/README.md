# Broadcasting

### STEP 1) Install Pusher to your Laravel project

- Run the following command to install pusher to your project

```bash
composer require pusher/pusher-php-server
```

### STEP 2) Create a new account in Pusher

- Navigate to https://pusher.com

- Create a new Channel

- Fill your laravel app details

- Replace your env files with the pusher connection data

- Change the `BROADCAST_DRIVER` configuration to `pusher`

- In the app.php app, uncomment the following line

```php
App\Providers\BroadcastServiceProvider::class,
```


### STEP 3) Create a new Event

- Run the following command to create a new Event

```bash
php artisan make:event MessageNotificationEvent 
```

- Implement the `ShouldBroadcast` interface to the created event

- Add a protected property to receive the `$message` as parameter in the constructor

```php
public $message;
public function __construct($message)
{
    $this->message = $message;
}
```

- Replace the `broadcastOn` function with the following code

```php
public function broadcastOn()
{
    return new Channel('notification');
}
```

### STEP 4) Install Laravel echo

- Install NodeJs
```bash
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs
```
- Install npm
```bash
curl -qL https://www.npmjs.com/install.sh | sh
```
- Verify installation
```bash
nodejs --version
```
```bash
npm --version
```

- Run the following command to install laravel echo
```bash
npm install pusher-js laravel-echo --save
```


### STEP 5) Add the routes 

- In `web.php` file add the following route

```php
Route::get('/listen', function()
{
    return view('listen');
});
```

- In `api.php` file add the following route

```php
Route::get('/event', function()
{
    event(new MessageNotificationEvent('Test broadcast message'));
});
```

### STEP 6) Create a new view 

- Create a new view with the name `listen.blade.php` and put the following code

```html
<!DOCTYPE html>
    <html>
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
        <title>Listen</title>
    
    </head>
    <body>
        @vite('resources/js/app.js')
    </body>
</html>
```

### STEP 7) Create the channel connection on Client side

- In `app.js` file add the following code

```javascript
window.Echo.channel('notification')
    .listen('MessageNotificationEvent', (e) => {
        alert('Notification received in real time!!');
    });
```

