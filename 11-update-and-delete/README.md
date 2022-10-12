# Update and Delete

### STEP 1) Add an edit link in the `movie.blade.php`

Add the following code in the form

```html
  <a href="/movies/{{$Movie->id}}/edit">Edit Movie</a>
```

### STEP 2) Create a new view `movie-edit.blade.php`

Add the following code

```html
 @extends('layout')

@section('content')
    <h1>Edit Movie: {{$Movie->Title}}</h1>
    <br />
    <form method="POST" action="/movies/{{$Movie->id}}" enctype="multipart/form-data">
        @csrf
        @method('PUT')
        <div>
            <span>
                Title
            </span>
            <input type="text" name="title" value="{{$Movie->Title}}" />
            @error('title')
                <span style="color: red;">{{$message}}</span>
            @enderror
        </div>
        <br />
        <div>
            <span>
                Year
            </span>
            <input type="text" name="year" value="{{$Movie->Year}}" />
            @error('year')
            <span style="color: red;">{{$message}}</span>
            @enderror
        </div>
        <br />
        <div>
            <span>
                Genre
            </span>
            <input type="text" name="genre" value="{{$Movie->Genre}}" />
            @error('genre')
            <span style="color: red;">{{$message}}</span>
        @enderror
        </div>
        <br />
        <div>
            <span>
                Director
            </span>
            <input type="text" name="director" value="{{$Movie->Director}}" />
            @error('director')
            <span style="color: red;">{{$message}}</span>
        @enderror
        </div>
        <br />
        <div>
            <span>
                Producer
            </span>
            <input type="text" name="producer" value="{{$Movie->Producer}}" />
            @error('producer')
            <span style="color: red;">{{$message}}</span>
        @enderror
        </div>
        <br />
        <div>
            <span>
                Actors
            </span>
            <input type="text" name="actors" value="{{$Movie->Actors}}" />
            @error('actors')
            <span style="color: red;">{{$message}}</span>
            @enderror
        </div>
        <br />
        <div>
            <span>
                Description
            </span>
            <textarea rows="4" name="description">
                {{$Movie['Description']}}
            </textarea>
            @error('description')
            <span style="color: red;">{{$message}}</span>
            @enderror
        </div>
        <br />
        <div>
            <span>
                Logo
            </span>
            <input type="file" name="logo"></input>
            <img class="img-thumbnail" src="{{$Movie->Logo ? asset('storage/' . $Movie['Logo']) : asset('/images/no-image.png')}}" />

            @error('logo')
                <span style="color: red;">{{$message}}</span>
            @enderror
        </div>
        <br />
        <div>
            <button type="submit">Update</button>
        </div>
    </form>
@endsection
```

### STEP 3) Add Update functions on the `MovieController`

Add the following code at the bottom of the file

```php
 `   public function update(Request $request, Movie $movie) {
       
        $formFields = $request->validate([
            'title' => 'required',
            'year' => 'required',
            'genre' => 'required',
            'actors' => 'required',
            'director' => 'required',
            'producer' => 'required',
            'description' => 'required'
        ]);
      
        if($request->hasFile('logo'))
        {
            $formFields['logo'] = $request->file('logo')->store('logos', 'public');
        }
       
        $movie->update($formFields);

        return redirect('/movies')->with('message', 'Movie updated successfully!');
    }

    public function edit(Movie $movie)
    {
        return view('movie-edit', ['Movie' => $movie]);

    }
```

### STEP 4) Add the routes for the edit/update endpoints

Navigate to the Web routes

```php
   
Route::get('/movies/{movie}/edit', [MovieController::class, 'edit']);

Route::put('/movies/{movie}', [MovieController::class, 'update']);
```



### STEP 5) Add a delete button in the `movie.blade.php`

Add the following code in the form

```html
 <form method="POST" action="/movies/{{$Movie->id}}">
        @csrf
        @method('DELETE')
        <button type="submit">Delete</button>
  </form>
```

### STEP 6) Add the routes for delete endpoint

Navigate to the Web routes

```php
   
Route::delete('/movies/{movie}', [MovieController::class, 'destroy']);

```

### STEP 6)  Add Delete function on the `MovieController`

Add the following code at the bottom of the file

```php
   
 public function destroy(Movie $movie)
  {
        $movie->delete();
        return redirect('/movies')->with('message', 'Movie deleted successfully!');
  }
```

