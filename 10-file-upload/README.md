# File Upload

### STEP 1) Add the file input in the `movie.create.blade.php`

Add the following code in the form

```php
<div>
   <span>
      Logo
   </span>
   <input type="file" name="logo"></input>
   @error('logo')
     <span style="color: red;">{{$message}}</span>
   @enderror
</div>
```

### STEP 2) Change the enctype for the create form

Add the enctype as `multipart/form-data`

```php
  <form method="POST" action="/movies" enctype="multipart/form-data">
```

### STEP 3) Change the storage system to Public 

Navigate to `filesystem.php` file and replace the default to use public

```php
 ` 'default' => env('FILESYSTEM_DISK', 'public'),
```

### STEP 4) Add a new column to store the file path in the database

In the migration `create_movies_table.php` file add a new Logo column 

```php
    Schema::create('movies', function (Blueprint $table) {
            $table->id();      
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

### STEP 5) Run the migration --seed command

Run the following command to run the migration and seed the database

```bash
php artisan migrate:refresh --seed 
```

### STEP 6) Add the file store in the `store` function on the MoviesController 

```php
if($request->hasFile('logo'))
{
   $formFields['logo'] = $request->file('logo')->store('logos', 'public');
}
```

### STEP 7) Add the image into the `movie-card.blade.php` component

```php
   <img class="img-thumbnail" src="{{$Movie->Logo ? asset('storage/' . $Movie['Logo']) : asset('/images/no-image.png')}}" />
```

Download https://prod-spinneys-cdn.azureedge.net/static/img/no-image-found.b1edc35f0fa6.png

Store the downloaded image into `public/images`

### STEP 8) Run the command to public storage link 

```bash
 php artisan storage:link
```

### STEP 7) Open the app on your Browser

```bash
  php artisan serve
```

http://127.0.0.1:8002/movies
