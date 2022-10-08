# Components and Controllers

### STEP 1) Create a components folder into the views folder

![image](https://user-images.githubusercontent.com/31894600/194683736-baea2ef8-72dc-4f62-92ce-72610df697f5.png)

Add following code

```php
@props(['Movie'])
<div>
    <h2>
        <a href="/movies/{{$Movie['id']}}">
            {{$Movie['Title']}} 
        </a>
    </h2>
    <h3>
        Year: <a href="/movies?year={{$Movie['Year']}}"> {{$Movie['Year']}} </a>
    </h3>
    <h3>
        Genre: <a href="/movies?genre={{$Movie['Genre']}}"> {{$Movie['Genre']}} </a>
    </h3>
    <h3>
        Director: <a href="/movies?director={{$Movie['Director']}}"> {{$Movie['Director']}} </a>
    </h3>
    <h3>
        Producer: {{$Movie['Producer']}}
    </h3>
    <p>
        {{$Movie['Description']}}
    </p>
</div>
```

### STEP 2) Use the component on the movies view

Replace the code in 'movies.blade.php' file with the following code

```php
<h1>{{$title}}</h1>
@foreach($movies as $Movie)
    <x-movie-card :Movie="$Movie" />
@endforeach
```

### STEP 3) Create a Movie Controller

Run the following command

```bash
php artisan make:controller MoviesController
```

A new file with be created in 'app/Http/Controllers'

![image](https://user-images.githubusercontent.com/31894600/194685997-20b41a6e-877c-461c-8a31-d059638fa696.png)


Replace all the file content with the following code

```php
<?php

namespace App\Http\Controllers;

use App\Models\Movie;

class MoviesController extends Controller
{
    public function index()
    {
        return view('movies', [
            'title' => 'Movies',
            'movies' => Movie::all()
        ]);
    }

    public function show(Movie $movie)
    {
        return view('movie', [
        
            'Movie' => $movie
        ]);

    }
}
```

### STEP 3) Change the Routes to use the new MoviesController

![image](https://user-images.githubusercontent.com/31894600/194686075-93bf31e4-9bc8-4091-9ee3-a74ad34605ba.png)

Replace the code in 'web.php' with the following code

```php

<?php

use App\Http\Controllers\MoviesController;
use Illuminate\Support\Facades\Route;
use App\Models\Movie;

Route::get('/movies', [MoviesController::class, 'index']);

Route::get('/movies/{movie}', [MoviesController::class, 'show']);

```
