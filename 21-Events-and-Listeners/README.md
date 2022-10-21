# Events and Listeners

### STEP 1) Create Migration for the Newsletter table

Run the following command

```bash
php artisan make:migration create_newsletters_table
```

![image](https://user-images.githubusercontent.com/31894600/196337378-09372b05-a9b4-4685-b4ef-8d1d4d46a99f.png)


### STEP 2) Edit the created Migration file


Replace the `up()` function with the following code

```php
  public function up()
    {
        Schema::create('newsletters', function (Blueprint $table) {
            $table->id();
            $table->string('email')->unique();
            $table->timestamps();
        });
    }
```


### STEP 3) Run the migration to create the table on MySQL

Run the following command

```bash
php artisan migrate
```

### STEP 4) Create and Eloquent Model for Newsletter

```bash
php artisan make:model Newsletter
```

- In the NewsLetter model add the email as fillable field

```php
protected $fillable = ['email'];
```

### STEP 5) Create a new Event

- Run the following command to create a new Event

```bash
php artisan make:event UserResgisteredEvent 
```
![image](https://user-images.githubusercontent.com/31894600/196337436-1081ef81-9c4b-433c-aa99-72c0d9fd783d.png)

- Add a protected property to receive the `$user` as parameter in the constructor

```php
public $user;
public function __construct($user)
{
    $this->user = $user;
}
```

![image](https://user-images.githubusercontent.com/31894600/196337475-d60248d3-74a5-45a3-ac4e-27d5b75f3308.png)


### STEP 6) Create a new Listener

- Run the following command to create a new Listener

```bash
php artisan make:listener AddToNewsletterListener
```

![image](https://user-images.githubusercontent.com/31894600/196337529-81d333d5-e497-4d57-8f5e-cd5c03fd18f2.png)


### STEP 7) Register the event

- In the `EventServiceProvider.php` class replace the `$listen` property with the following code

![image](https://user-images.githubusercontent.com/31894600/196337502-a0472e65-6f52-4760-898a-86bd066a4108.png)

```php
protected $listen = [
    UserResgisteredEvent::class => [
        AddToNewsletterListener::class
    ]
];
```

### STEP 8) Add the logic to execute in the listener

- In the `AddToNewsletterListener.php` class replace the `handle()` function with the following code

```php
 public function handle($event)
    {
        Newsletter::create([
            'email' => $event->user->email
        ]);
    }
```

### STEP 8) Invoke the event on the User creation

- In the `UserController.php` add the following line in the `store()` function

```php
event(new UserResgisteredEvent($user));
```

![image](https://user-images.githubusercontent.com/31894600/196339901-02354e96-4861-48e7-829a-301d9f3704b6.png)
