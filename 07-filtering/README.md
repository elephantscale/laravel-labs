# Filtering

### STEP 1) Add the filtering logic into the Movie Model

![image](https://user-images.githubusercontent.com/31894600/194688453-b378e79a-2192-452d-a2a5-ce8e697b4d1b.png)

Replace the following function

```php

    public function scopeFilter($query, Request $request)
    {
        if($request['year'] ?? false)
        {
            $query->where('year', '=', $request['year'] );
        }
        else 
        {
            if($request['genre'] ?? false)
            {
                $query->where('genre', '=', $request['genre'] );
            }
            else
            {
                if($request['director'] ?? false)
                {
                    $query->where('director', '=', $request['director'] );
                }
            }
        }
        if($request['search'] ?? false)
        {
            $query->where('title', 'like', '%' . $request['search'] . '%' )
              ->orWhere('description', 'like', '%' . $request['search'] . '%' )
              ->orWhere('director', 'like', '%' . $request['search'] . '%' )
              ->orWhere('producer', 'like', '%' . $request['search'] . '%' )
              ->orWhere('actors', 'like', '%' . $request['search'] . '%' );
        }
    }

```

### STEP 2) Add the filtering logic in the Movies Controller

Change the index function with the following code

```php

public function index()
    {
        return view('movies', [
            'title' => 'Movies',
            'movies' => Movie::latest()->filter(request())->get()
        ]);
    }

```

### STEP 3) Create a search component

Create a new file under the 'resources/views/components' with the name search.blade.php

![image](https://user-images.githubusercontent.com/31894600/194688924-cbd2331c-9add-4aea-81d3-a3d8bf8bb3ef.png)

Add the following code in the new created file

```php

<form action="/">
    <input type="text" name="search" />
    <button type="submit">Search</button>
</form>

```

### STEP 4) Add the search component into the 'movies.blade.php'

Add the following code

```php

<h1>{{$title}}</h1>
<x-search />
<br />
@foreach($movies as $Movie)
    <x-movie-card :Movie="$Movie" />
@endforeach

```
