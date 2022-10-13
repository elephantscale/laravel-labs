# User Login

### STEP 1) Create a `MovieFactory.php` class 

Add the following code

```php
<?php

namespace Database\Factories;

use Illuminate\Database\Eloquent\Factories\Factory;
use Illuminate\Support\Str;

/**
 * @extends \Illuminate\Database\Eloquent\Factories\Factory<\App\Models\Model>
 */
class MovieFactory extends Factory
{
    /**
     * Define the model's default state.
     *
     * @return array<string, mixed>
     */
    public function definition()
    {
        return [
            'Title' => $this->faker->sentence(),
            'Genre' => Str::random(10),
            'Director' => $this->faker->name(),
            'Producer' => $this->faker->name(),
            'Actors' => $this->faker->name(),
            'Year' => $this->faker->numberBetween(1910, 2022),
            'Description' => $this->faker->paragraph(5),
        ];
    }
}
```

### STEP 2) Add a new column to store the file path in the database

In the migration `create_movies_table.php` file add a new user_id column

```php
    Schema::create('movies', function (Blueprint $table) {
            $table->id();      
            $table->foreignId('user_id')->constrained()->onDelete('cascade');      
            $table->string('Title');
            $table->string('Logo')->nullable();
            $table->string('Genre');
            $table->string('Director');
            $table->string('Producer');
            $table->string('Actors');
            $table->integer('Year');
            $table->longText('Description');
            $table->timestamps();
        });
```

### STEP 3) Edit the `DatabaseSeeder.php` file

Replace the run method content with the following

```php
 $user = User::factory()->create([
           'name' => 'Jhon Doe',
           'email' => 'JhonD@gmail.com'
        ]);

 \App\Models\Movie::factory(15)->create([
      'user_id' => $user->id
  ]);
```


### STEP 4) Run the migration --seed command

Run the following command to run the migration and seed the database

```bash
php artisan migrate:refresh --seed 
```

### STEP 5) Add the users relationship in the `Movie.php` model

Add the following function

```php
public function user()
{
    return $this->belongsTo(User::class, 'user_id');
}
```

### STEP 6) Add the movies relationship in the `User.php` model

Add the following function

```php
public function movies()
{
    return $this->hasMany(Movie::class, 'user_id');
}
```

### STEP 8) Run tinker to see relations

```bash
  php artisan tinker
```

Run the following command to check the movies related to the user

```bash
\App\Models\User::first()->movies
```

### STEP 9) Open the app on your Browser

```bash
  php artisan serve
```

http://127.0.0.1:8002/movies
