#Jobs

### STEP 1) Create a new Mail Element

- Run the following command to create a new Mail

```bash
php artisan make:mail InstructionsMail
```

- Add the following public property
```php
public $subject = "Instructions Email";
```

- Change the `build` function with the following code

```php
 public function build()
    {
        return $this->view('instructions');
    }
```

- Create a new view with the name `instructions.blade.php` and put the following code

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
        <title>Instructions Email</title>
    </head>
    <body>
        <h1>  
            Instructions
        </h1>
        <p>In this email you will find all the instructions needed to use this web app</p>
    </body>
</html>
```


### STEP 2) Create a new Job

- Run the following command to create a new Event

```bash
php artisan make:job SendInstructionsEmailJob
```

- Add a protected property to receive the `$user` as parameter in the constructor

```php
public $user;
public function __construct($user)
{
    $this->user = $user;
}
```

- Replace the handle method with the following code

```php
public function handle()
{
    $mail = new InstructionsMail();
    Mail::to($this->user->email)->send($mail);
}
```

### STEP 3) Run Jub on the User creation

- In the `UserController.php` add the following line in the `store()` function

```php
SendInstructionsEmailJob::dispatch();
```