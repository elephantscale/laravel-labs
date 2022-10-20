# Jobs

### STEP 1) Create a new Mail Element

- Run the following command to create a new Mail

```bash
php artisan make:mail NewsletterMail
```

- Add the following public property
```php
public $subject = "Newsletter Email";
```

- Change the `build` function with the following code

```php
 public function build()
    {
        return $this->view('newsletter');
    }
```

- Create a new view with the name `newsletter.blade.php` and put the following code


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

- Change the `$signature` and `$description` properties
 
```php
protected $signature = 'send_newsletter:task';
protected $description = 'Send a Newsletter email to all subscribed users';
```

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

- Run the following command to get the list of commands

```bash
php artisan schedule:list
```

### STEP 4) Run the Schedule

- Run the following command to run the schedule work

```bash
php artisan schedule:work
```


