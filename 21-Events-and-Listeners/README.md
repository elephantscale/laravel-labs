# Events and Listeners

### STEP 1) Create Migration for the Newsletter table

Run the following command

```bash
php artisan make:migration create_newsletters_table
```

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

### STEP 4) Create a new Event

- Run the following command to create a new Event

```bash
php artisan make:event UserResgisteredEvent 
```

- Add a protected property to receive the `$user` as parameter in the constructor

```php
public $user;
public function __construct($user)
{
    $this->user = $user;
}
```

### STEP 5) Create a new Listener

- Run the following command to create a new Event

```bash
php artisan make:listener AddToNewsletterListener
```

### STEP 6) Register the event

- In the `EventServiceProvider.php` class replace the `$listen` property with the following code

```php
protected $listen = [
    UserResgisteredEvent::class => [
        AddToNewsletterListener::class
    ]
];
```

### STEP 7) Add the logic to execute in the listener

- In the `AddToNewsletterListener.php` class replace the `handle()` function with the following code

```php
 public function handle($event)
    {
        Newsletter::create([
            'email' => $event->user->email
        ]);
    }
```