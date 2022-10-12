# User Login

### STEP 1) Create a new view `login.blade.php`

![image](https://user-images.githubusercontent.com/31894600/195363590-9f4f5bba-e877-4e01-8eed-43e375f1a76e.png)

Add the following code

```html
@extends('layout')

@section('content')

<h1>Login</h1>
<br />
<form method="POST" action="/users/authenticate">
    @csrf
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
        <button type="submit">Login</button>
    </div>
</form>

@endsection

```

### STEP 2) Add login functions in the `UserController`

Add the following code

```php
 public function login()
  {
     return view('login');
  }
```

### STEP 4) Add the routes for the registration endpoints

Navigate to the Web routes

```php
   
Route::get('/login', [UserController::class, 'login']);

```

### STEP 5) Add authenticate method in the `UserController`

Add the following code

```php
 public function authenticate(Request $request)
{
    $formFields = $request->validate([
    'email' => ['required', 'email'],
    'password' => 'required'
    ]);
    
    if(auth()->attempt($formFields))
    {
    $request->session()->regenerate();
    return redirect('/movies')->with('message', 'You are now logged in!');
    
    }
    return redirect('/login')->withErrors(['email'=> 'Invalid Credentials'])->onlyInput('email');
}

```

### STEP 5) Add the routes for authenticate endpoints

Navigate to the Web routes

```php
Route::post('/users/authenticate', [UserController::class, 'authenticate']);
```

### STEP 6) Open the app on your Browser

```bash
  php artisan serve
```

http://127.0.0.1:8002/movies
