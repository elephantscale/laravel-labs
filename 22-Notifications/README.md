# Notifications

### STEP 1) Configure MailTrap

- Create an account in https://mailtrap.io/


- In the Home click in the Setup Inbox Button

![image](https://user-images.githubusercontent.com/31894600/196341572-2f906d25-be01-4ead-a36c-c3d524dfcc7c.png)

- Select the Laravel 7+ Integration

![image](https://user-images.githubusercontent.com/31894600/196341626-848f26aa-bdc2-458b-929d-f90fe73d055e.png)

- Copy the connection values

![image](https://user-images.githubusercontent.com/31894600/196341651-7f4c7af6-f184-43ca-a50f-b4f242a2c399.png)

- in the `env` file, replace the email connection information with the mailtrap connection values

![image](https://user-images.githubusercontent.com/31894600/196341666-d409407b-3ba4-408d-932c-1821dbc0d5c2.png)

### STEP 2) Create a new Event

- Run the following command to create a new Notification

```bash
php artisan make:notification SendRegistrationEmail 
```

![image](https://user-images.githubusercontent.com/31894600/196347652-676e68fa-6609-4942-96bc-bc399f053661.png)


- Add a protected property to receive the `$user` as parameter in the constructor

```php
public $user;
public function __construct($user)
{
    $this->user = $user;
}
```

![image](https://user-images.githubusercontent.com/31894600/196347694-f953e915-efc7-4c1a-84ea-3a69442a0c35.png)


- Replace the `toMail()` function with the following code

```php
public function toMail($notifiable)
{
    return (new MailMessage)
         ->line('Dear '. $this->user->name . '. This is a notification to let you know that you were registered to our site.')
         ->action('You were succesfully registered' ., url('/'))
         ->line('Thank you for using our application!');
    }
```

- Add `database` in the `via()` function return array

```php
  return ['mail', 'database'];
```

![image](https://user-images.githubusercontent.com/31894600/196347803-4ee5739c-3377-4afc-a46f-b528a29886a0.png)


### STEP 3) Send Notification on the User creation

- In the `UserController.php` add the following line in the `store()` function

```php
$user->notify(new SendRegistrationEmail($user));
```

![image](https://user-images.githubusercontent.com/31894600/196347782-46684acf-fd19-4a97-82f8-11b8c1f87e68.png)


### STEP 4) Create the Notification table Migration


- Run the following command to create a database migration to create the notifications table

```bash
php artisan notification:table
```

![image](https://user-images.githubusercontent.com/31894600/196347740-b13fec82-b89b-4fe1-aa7f-26756c3a8322.png)


- Run the following command to run the migration and seed the database

```bash
php artisan migrate:refresh --seed 
```
