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

### STEP 3)  Navigate to views folder, rename it to movies.blade.php and remove all the file content

![image](https://user-images.githubusercontent.com/31894600/193735502-29aa3f76-7005-4cc0-a651-cdcd55d18d33.png)

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

![image](https://user-images.githubusercontent.com/31894600/193730158-c03e8295-1c09-4828-a1f3-7505ac2991c5.png)
