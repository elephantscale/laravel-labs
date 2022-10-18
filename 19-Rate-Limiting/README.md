# Implement Rate Limit

### STEP 1) Add token authentication to the API

- In the `create_users_table.php` file, replace the `up` function with the following code

![image](https://user-images.githubusercontent.com/31894600/196095253-31a10e12-0799-4bbc-a4ef-89f7ad9ce828.png)

```php
 public function up()
    {
        Schema::create('users', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->string('email')->unique();
            $table->timestamp('email_verified_at')->nullable();
            $table->string('password');
            $table->string('api_token')->unique()->nullable()->default(null);
            $table->string('rate_limit')->default(strval(rand(3, 10)));
            $table->rememberToken();
            $table->timestamps();
        });
    }
 ```

- In the `DatabaseSeeder.php` replace the user seed with the following code

 ```php
  $user = User::factory()->create([
            'name' => 'Jhon Doe',
            'email' => 'JhonD@gmail.com',
            'api_token'=> Str::random(80),
            'rate_limit'=> strval(rand(3, 10))
        ]);
 ```

- Run the following command to run the migration and seed the database

```bash
php artisan migrate:refresh --seed 
```

- In the `config\auth.php` file add a new guard

 ```php
'api' => [
     'driver' => 'token',
     'provider' => 'users'
     ]
 ```
 
 ![image](https://user-images.githubusercontent.com/31894600/196095283-3ea4a77e-e986-4aac-a68e-07c4e7756335.png)


### STEP 2) Add the Throttle to the movies Endpoint

In the `routes\api.php` replace the movies endpoint with

 ```php
Route::get('/movies', [MoviesController::class, 'index'])->middleware('auth:api', 'throttle:rate_limit,1');
 ```

### STEP 3) Add a Rate Limiter


In the `configureRateLimiting()` function on `RouteServiceProvider.php`file add the following code 

 ```php
 RateLimiter::for('movies_limiter', function (Request $request) {
            return Limit::perMinute(2);
    }); 
```

### STEP 4) Test the endpoint using Postman

- Get the api_token from the database

![image](https://user-images.githubusercontent.com/31894600/196324328-3e1c5d88-b3ff-4fcc-8575-50b0601ac06f.png)

- Configure the Token in Postman as the following image
_____________________________________________________________________________________________

![image](https://user-images.githubusercontent.com/31894600/196324505-769a1250-ed1e-441e-b87a-708607201719.png)


- Send the request mutiple times until get a 429 status error
_____________________________________________________________________________________________

![image](https://user-images.githubusercontent.com/31894600/196324866-c897a37a-fe43-466e-95da-1c8a2a825494.png)


