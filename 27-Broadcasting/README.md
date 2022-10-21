# Broadcasting

### STEP 1) Install Pusher to your Laravel project

- Run the following command to install pusher to your project

```bash
composer require pusher/pusher-php-server
```

### STEP 2) Create a new account in Pusher

- Navigate to https://pusher.com

![image](https://user-images.githubusercontent.com/31894600/197119281-f3dc01e1-f0d0-4d77-b073-fca6f5b5dc34.png)

- Create a new Channel

![image](https://user-images.githubusercontent.com/31894600/197119319-b5359035-1c7a-4a80-9b2f-654882eb3b78.png)

- Fill your laravel app details

![image](https://user-images.githubusercontent.com/31894600/197119370-8b879b8a-08fe-44f0-b8fa-f7adf9c38cca.png)

- Replace your env files with the pusher connection data

![image](https://user-images.githubusercontent.com/31894600/197119423-28619bc6-6e79-4e41-af70-003a4a5063ac.png)

![image](https://user-images.githubusercontent.com/31894600/197119464-a8f81128-6f5e-437e-96bb-d07d13b5c82e.png)

- Change the `BROADCAST_DRIVER` configuration to `pusher`

![image](https://user-images.githubusercontent.com/31894600/197119501-f8829abb-80b9-4737-a7d3-d1ee88787295.png)

- In the app.php app, uncomment the following line

```php
App\Providers\BroadcastServiceProvider::class,
```
![image](https://user-images.githubusercontent.com/31894600/197119533-a2132b53-b695-421d-8754-e89b0601355d.png)

### STEP 3) Create a new Event

- Run the following command to create a new Event

```bash
php artisan make:event MessageNotificationEvent 
```
![image](https://user-images.githubusercontent.com/31894600/197119560-15a5c634-1ae6-44c5-9257-d85ba7b39308.png)

- Implement the `ShouldBroadcast` interface to the created event

![image](https://user-images.githubusercontent.com/31894600/197119579-9b72bb58-e9a8-40de-a243-0c76e9954269.png)

- Add a protected property to receive the `$message` as parameter in the constructor

```php
public $message;
public function __construct($message)
{
    $this->message = $message;
}
```

![image](https://user-images.githubusercontent.com/31894600/197119608-4ac22837-6be2-41c4-8d3f-30d5d4e5fe94.png)

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

![image](https://user-images.githubusercontent.com/31894600/197119680-a7c35517-fc16-4991-be78-7fad8e15e0d4.png)

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

![image](https://user-images.githubusercontent.com/31894600/197119710-d5b178ff-36c9-4b8b-bb48-89f3106e3a78.png)

```javascript
window.Echo.channel('notification')
    .listen('MessageNotificationEvent', (e) => {
        alert('Notification received in real time!!');
    });
```

