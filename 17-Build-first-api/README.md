# Create an API for Movies

### STEP 1) Modify the Movies Controller to store the user id

Run the following command to create a new API controller 

```bash
php artisan make:controller Api/MoviesController
```

### STEP 2) Add the first endpoint

Add the following code
```php
 public function index()
 {
    return Movie::all();
 }
```

## STEP 3) Add the new route in the Api Route

Add the following code

```php
Route::get('/movies', [MoviesController::class, 'index']);
```

### STEP 4) Install Postman

Run the following commands

```bash
wget https://dl.pstmn.io/download/latest/linux64
```
```bash
sudo tar -xvf linux64 -C /usr/bin
```
```bash
echo 'export PATH="$PATH:/usr/bin/Postman"' >> ~/.bashrc
```
```bash
postman
```
```bash
sudo nano /usr/share/applications/Postman.desktop
```

Paste the following text
```bash
[Desktop Entry]
Name=Postman API Tool
GenericName=Postman
Comment=Testing API
Exec=/usr/bin/Postman/Postman
Terminal=false
X-MultipleArgs=false
Type=Application
Icon=/usr/bin/Postman/app/resources/app/assets/icon.png
StartupWMClass=Postman
StartupNotify=true
```
Once done, save the file (Ctrl + S) and Exit (Ctrl + X)

Search Postman Application and run it


### STEP 5) Test the Movies API in Postman

Run the Movies App

```bash
php artisan serve
```

In Postman do a Get to http://127.0.0.1:8002/api/movies/

### STEP 6) Transform with API Resources

Run the following command to create an API Resource

```bash
php artisan make:resource MoviesResource
 ```

Replace the existing ToArray function with the following code

```php
public function toArray($request)
    {
        return [
            'id' => $this->id,
            'tittle' => $this->Title,
            'year' => $this->Year,
            'description' => $this->Description,
            'creation Date' => $this->created_at->format('m-dd-yyyy')
            
        ];
    }
 ```

Test in Postman



In the `AppServiceProvider.php` add the following line in the `boot` method

```php
JsonResource::withoutWrapping();
 ```

Test in Postman



### STEP 7) Open the app on your Browser

```bash
  php artisan serve
```

http://127.0.0.1:8002/movies
