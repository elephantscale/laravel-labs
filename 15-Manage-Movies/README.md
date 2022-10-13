# Manage Movies

### STEP 1) Modify the Movies Controller to store the user id

In the store function, add the following code

```php
$formFields['user_id'] = auth()->id();
```

### STEP 2) Add a new view to manage movies

Create a new view `movies-manage.blade.php`

```html
@extends('layout')

@section('content')
<a href="/movies/create">Create new Movie</a>
<br />
<br />
<table class="table">
    <thead>
    <tr>
        <th scope="col">#</th>
        <th scope="col">Title</th>
        <th scope="col">year</th>
        <th scope="col"></th>
    </tr>
    </thead>
    <tbody>
    @foreach($Movies as $Movie)
    <tr>
        <th scope="row">1</th>
        <td>{{$Movie['Title']}}</td>
        <td>{{$Movie['Year']}}</td>
        <td>
            <a href="/movies/{{$Movie->id}}/edit">Edit</a>
            <br />
            <form method="POST" action="/movies/{{$Movie->id}}">
                @csrf
                @method('DELETE')
                <button type="submit">Delete</button>
            </form>
        </td>
    </tr>
    @endforeach
    </tbody>
</table>
@endsection   
```

## STEP 3) Add the new routes the manage view

Add the following code

```php

Route::get('/movies/manage', [MovieController::class, 'manage'])->middleware('auth');

```

### STEP 3) Add the manage function in `MoviesController.php` 

Add the following code

```php
    public function manage()
    {
        return view('movies-manage', ['Movies' => auth()->user()->movies()->get()]);
    }
```

### STEP 4) Add the user_id field as fillable in the 'Movie' model

Add the following code in the Movie Model

```php
protected $fillable = ['title', 'year', 'description', 'genre', 'director', 'producer', 'actors', 'logo', 'user_id'];
```

### STEP 5) Add authorization validation on Movie Update and Delete

Add the following code in `MoviesController.php` 

```php
 if($movie -> user_id != auth()->id())
 {
     abort(403, 'Unauthorized Action');    
 }
 ```

### STEP 6) Open the app on your Browser

```bash
  php artisan serve
```

http://127.0.0.1:8002/movies
