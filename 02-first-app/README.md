# First Laravel App

### STEP 1) Install VS Code


```bash
  sudo snap install --classic code
```

### STEP 2) Open Project using VS Code

```bash
  code .
```
![image](https://user-images.githubusercontent.com/31894600/193714528-d404a231-bd97-4058-8126-ea5d4899d48b.png)

### STEP 3) Rename file

* Navigate to views folder, rename `welcome.blade.php` to `movies.blade.php`

![image](https://user-images.githubusercontent.com/31894600/193735502-29aa3f76-7005-4cc0-a651-cdcd55d18d33.png)

Replace the content with the following code

```php
    <h1>{{$title}}</h1>
    @foreach($movies as $movie)
    <h2>
        {{$movie['name']}} - {{$movie['year']}}
    </h2>
    @endforeach
```
### STEP 4) Navigate to Web Routes

![image](https://user-images.githubusercontent.com/31894600/193736454-0d6ddfa6-5f42-475e-b4dd-d9f584513bb2.png)

Add the following code

```php
  Route::get('/movies', function () {
    return view('movies', [
        'title' =>'Movies',
        'movies' => [
            [
                'name' => 'Scarface',
                'year' => 1983
            ],
            [
                'name' => 'Avatar',
                'year' => 2009
            ],
            [
                'name' => 'Avengers',
                'year' => 2012
            ]
            
        ]
    ]);
});
```
### STEP 5) Open the app on your Browser

```bash
  php artisan serve
```

 http://127.0.0.1:8002/movies
 
 
![image](https://user-images.githubusercontent.com/31894600/193737662-1f73d02a-55ad-49a0-b8e6-1dc97cf1eaf3.png)

