# Create new movies

### STEP 1) Create new view with the name 'movie-create.blade.php'

![image](https://user-images.githubusercontent.com/31894600/194692288-50aa2ea8-5ac2-4a28-9d92-529a91985a27.png)

Add the following code

```php

<h1>New Movie</h1>
<br />
<form method="POST" action="/movies">
    @csrf
    <div>
        <span>
            Title
        </span>
        <input type="text" name="title" />
    </div>
    <br />
    <div>
        <span>
            Year
        </span>
        <input type="text" name="year" />
    </div>
    <br />
    <div>
        <span>
            Genre
        </span>
        <input type="text" name="genre" />
    </div>
    <br />
    <div>
        <span>
            Director
        </span>
        <input type="text" name="director" />
    </div>
    <br />
    <div>
        <span>
            Producer
        </span>
        <input type="text" name="producer" />
    </div>
    <br />
    <div>
        <span>
            Actors
        </span>
        <input type="text" name="actors" />
    </div>
    <br />
    <div>
        <span>
            Description
        </span>
        <textarea rows="4" name="description" ></textarea>
    </div>
    <br />
    <div>
        <button type="submit">Save</button>
    </div>
</form>

```

### STEP 2) Add the new routes for the create view and the save action

```php

Route::post('/movies', [MoviesController::class, 'save']);

Route::get('/movies/create', [MoviesController::class, 'create']);

```

### STEP 3) Modify the 'MoviesController' with the view show and the save logic


```php

   public function create()
    {
        return view('movie-create');

    }

  
    public function save(Request $request) {
        $formFields = $request->validate([
            'title' => 'required',
            'year' => 'required',
            'genre' => 'required',
            'actors' => 'required',
            'director' => 'required',
            'producer' => 'required',
            'description' => 'required'
        ]);

        Movie::create($formFields);

        return redirect('/')->with('message', 'Movie created successfully!');
    }
```

### STEP 4) Add the field as fillable in the 'Movie' model

Add the following code in the Movie Model

```php
protected $fillable = ['title', 'year', 'description', 'genre', 'director', 'producer', 'actors'];
```

### STEP 5) Add a link to the create form from the movies list

Add the following line in the 'movies.blade.php' view

```php
<a href="/movies/create">Create new Movie</a>
```

![image](https://user-images.githubusercontent.com/31894600/194693808-6cca3ed9-c834-4338-b6e9-ba8e3059d1f2.png)
