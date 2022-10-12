# User Registration

### STEP 1) Create the Users Controller

Run the following command

```bash
php artisan make:controller UserController
```

### STEP 2) Create a new view `register.blade.php`

Add the following code

```html
 @extends('layout')

@section('content')

<h1>Register</h1>
<br />
<form method="POST" action="/users">
    @csrf
    <div>
        <span>
            Name
        </span>
        <input type="text" name="name" value="{{old('name')}}" />
        @error('name')
        <span style="color: red;">{{$message}}</span>
        @enderror
    </div>
    <br />
    <div>
        <span>
            Email
        </span>
        <input type="text" name="email" value="{{old('email')}}" />
        @error('email')
        <span style="color: red;">{{$message}}</span>
        @enderror
    </div>
    <br />
    <div>
        <span>
            Password
        </span>
        <input type="password" name="password" value="{{old('password')}}" />
        @error('password')
        <span style="color: red;">{{$message}}</span>
        @enderror
    </div>
    <br />
    <div>
        <span>
            Confirm Password
        </span>
        <input type="password" name="password_confirmation" value="{{old('password2')}}" />
        @error('password_confirmation')
        <span style="color: red;">{{$message}}</span>
        @enderror
    </div>

    <br />
    <div>
        <button type="submit">Register</button>
    </div>
</form>

@endsection
```

### STEP 3) Add registration functions on the `UserController`

Add the following code 

```php
 `  public function create()
  {
     return view('register');
  }

  public function store(Request $request) {
    $formFields = $request->validate([
        'name' => ['required', 'min:3'],
        'email' => ['required', 'email', Rule::unique('users', 'email')],
        'password' => 'required|confirmed|min:6'
    ]);
  
    $formFields['password'] = bcrypt($formFields['password']);

    $user = User::create( $formFields);

    auth() -> login($user);

    return redirect('/movies')->with('message', 'User registered and Logged in!');
  }
```

### STEP 4) Add the routes for the registration endpoints

Navigate to the Web routes

```php
   
Route::get('/register', [UserController::class, 'create']);

Route::post('/users', [UserController::class, 'store']);
```



### STEP 5) Add registration links in the `layout.blade.php`

Add the following code

```html
<div>
    <a href="/register">Register</a>
    <a href="/login">Login</a>
</div>

```

### STEP 6) Add registration links in the `layout.blade.php`

Add the following code

```html
<div>
    <a href="/register">Register</a>
    <a href="/login">Login</a>
</div>

```


### STEP 7) Add registration functions on the `UserController`

Add the following code

```php
  public function logout(Request $request)
  {
    auth() -> logout();
    
    $request -> session() -> invalidate();
    $request -> session() -> regenerateToken();

    return redirect('/movies')->with('message', 'You have been Logged out!');
  }
```

### STEP 8) Add the routes for the logout endpoints

Navigate to the Web routes

```php
Route::post('/logout', [UserController::class, 'logout']);
```

### STEP 9) Add the Logout button and the Auth links

Add the following code

```html
 <div>
    @auth
    <h3>Welcome {{auth()->user()->name}}</h3>
    <form method="POST" action="/logout">
        @csrf
        <button type="submit">
            Logout
        </button>
    </form>
    @else
    <a href="/register">Register</a>
    <a href="/login">Login</a>
    @endauth
</div>
```

### STEP 10) Open the app on your Browser

```bash
  php artisan serve
```

http://127.0.0.1:8002/movies
