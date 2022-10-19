# Jobs

### STEP 1) Create a new Mail Element

- Run the following command to create a new Mail

```bash
php artisan make:mail InstructionsMail
```

![image](https://user-images.githubusercontent.com/31894600/196596111-f80905ef-c3a8-44b8-809c-8e89e6c5ef88.png)


- Add the following public property
```php
public $subject = "Instructions Email";
```
![image](https://user-images.githubusercontent.com/31894600/196596176-f989cfff-ff47-4677-b568-e36b480ac24e.png)


- Change the `build` function with the following code

```php
 public function build()
    {
        return $this->view('instructions');
    }
```

- Create a new view with the name `instructions.blade.php` and put the following code

![image](https://user-images.githubusercontent.com/31894600/196596158-c9530802-4d7d-4a8d-b575-649071674535.png)

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

![image](https://user-images.githubusercontent.com/31894600/196596002-3c08aa9f-3af5-4762-90c5-b411f62ad96b.png)


- Add a protected property to receive the `$user` as parameter in the constructor

```php
public $user;
public function __construct($user)
{
    $this->user = $user;
}
```

![image](https://user-images.githubusercontent.com/31894600/196596019-596dda9d-faa1-49f7-8579-7a1cbb9089e5.png)

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
SendInstructionsEmailJob::dispatch($user);
```
![image](https://user-images.githubusercontent.com/31894600/196596096-38049e37-356e-4ec7-abff-92695bfc4f36.png)

