# Jobs

### STEP 1) Create a new Mail Element

- Run the following command to create a new Mail

```bash
php artisan make:mail NewsletterMail
```
![image](https://user-images.githubusercontent.com/31894600/196852819-c74735bb-e334-4ae7-8a0c-016351c9368d.png)

- Add the following public property
```php
public $subject = "Newsletter Email";
```
![image](https://user-images.githubusercontent.com/31894600/196852841-e221c555-760f-47c8-ab72-b9b377ed0be5.png)


- Change the `build` function with the following code

```php
 public function build()
    {
        return $this->view('newsletter');
    }
```

- Create a new view with the name `newsletter.blade.php` and put the following code

![image](https://user-images.githubusercontent.com/31894600/196852858-7aeb7fdf-84ae-4dc0-ac50-15132372df87.png)

```html
<!DOCTYPE html>
    <html>
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
        <title>Newsletter Email</title>
    </head>
    <body>
        <h1>
            Newsletter
        </h1>
        <p>In this email you will find all Newsletter infoemation on a Daily basis</p>
    </body>
</html>
```

### STEP 2) Create a new Command

- Run the following command to create a new Event

```bash
php artisan make:command SendNewletterEmailCommand 
```

![image](https://user-images.githubusercontent.com/31894600/196852694-f52e99bb-6b7e-455f-8ac0-15289056d914.png)


- Change the `$signature` and `$description` properties
 
```php
protected $signature = 'send_newsletter:task';
protected $description = 'Send a Newsletter email to all subscribed users';
```

![image](https://user-images.githubusercontent.com/31894600/196852714-1325f172-26eb-4713-9b7a-436c98dd1f4e.png)


- Replace the `handle()` function with the following code

```php
public function handle()
    {
        $newsletters = Newsletter::all();
        foreach($newsletters as $newsletter)
        {
            $mail = new NewsletterMail();
            Mail::to($newsletter->email)->send($mail);
        }

        return Command::SUCCESS;
    }
```

### STEP 3) Add the command to the Kernel Schedule

- In the `Kernel.php` file add the following line in the `schedule()` function

```php
  $schedule->command('send_newsletter:task')->everyMinute()->withoutOverlapping();
```

![image](https://user-images.githubusercontent.com/31894600/196852766-edcbfab6-5fa4-4f0e-a1dc-24e9e8be29f4.png)

- Run the following command to get the list of commands

```bash
php artisan schedule:list
```

![image](https://user-images.githubusercontent.com/31894600/196852793-91d91a44-10f8-49aa-b884-96903066b78f.png)


### STEP 4) Run the Schedule

- Run the following command to run the schedule work

```bash
php artisan schedule:work
```

![image](https://user-images.githubusercontent.com/31894600/196852881-cb8b4322-5af0-415a-9cad-d10d6cdcddf6.png)



