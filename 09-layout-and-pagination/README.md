# Layout and Pagination

### STEP 1) Create new view with the name 'layout.blade.php'

Add the following code

```php
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
        <!-- Bootstrap CSS -->
        <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.3.1/dist/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
        <title>Movies</title>
    </head>
    <body>
        @yield('content')
    </body>
</html>
```

### STEP 2) Add Layout to your current views

Edit your files `movies.blade.php`, `movie.blade.php` and `movie.create.blade.php`

Surround the existing content with the following

```php
@extends('layout')

@section('content')
...
@endsection
```

### STEP 3) Add Pagination to you Controller

Change the `index` function with the following

```php
 public function index()
    {
       
        return view('movies', [
            'title' => 'Movies',
            'movies' => Movie::latest()->filter(request())->paginate(3)
        ]);
    }
```

### STEP 4) Add Styles and the pagination control on your movies list

Edit the `movies.blade.php` with the following

```php
`@extends('layout')

@section('content')

    @if(session()->has('message'))
        <label>{{session('message')}}</label>
    @endif

    <h1>{{$title}}</h1>
    <a href="/movies/create">Create new Movie</a>
    <br />
    <br />
    <x-search />
    <br />
    {{$movies->links("pagination::bootstrap-4")}}
    <br />
    <div class="container">
        <div class="row">
            @foreach($movies as $Movie)
            <div class="col-4">
                <x-movie-card :Movie="$Movie"  />
            </div>
            @endforeach
        </div>
      </div>
@endsection
```



