# Create an API for Movies

### STEP 1) Create a new API Controller for Movies

Run the following command to create a new API controller 

```bash
php artisan make:controller Api/MoviesController
```

![image](https://user-images.githubusercontent.com/31894600/196013751-a4a470b7-63f0-4f4b-9683-cbb2a516ae78.png)

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

![image](https://user-images.githubusercontent.com/31894600/196013757-59293634-6784-4021-98e8-de6fff8574c4.png)

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

![image](https://user-images.githubusercontent.com/31894600/196013787-134f3cfc-e045-4ad3-80aa-3692aebc5095.png)


### STEP 5) Test the Movies API in Postman

Run the Movies App

```bash
php artisan serve
```

In Postman do a Get to http://127.0.0.1:8002/api/movies/

![image](https://user-images.githubusercontent.com/31894600/196013795-1f5ad0d4-c602-4e1d-882e-6a79b1be21e7.png)

### STEP 6) Transform with API Resources

Run the following command to create an API Resource

```bash
php artisan make:resource MoviesResource
 ```

![image](https://user-images.githubusercontent.com/31894600/196013801-79d94fdb-4eca-4994-a79b-686984d2114f.png)

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

![image](https://user-images.githubusercontent.com/31894600/196013826-710ce9f6-cfdd-49a7-905d-782dad6658ee.png)

In the `AppServiceProvider.php` add the following line in the `boot` method

```php
JsonResource::withoutWrapping();
 ```

Test in Postman

![image](https://user-images.githubusercontent.com/31894600/196013839-3707efeb-d329-4ff9-a8d6-6fa48235c53c.png)


