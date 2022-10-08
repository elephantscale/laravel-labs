# Model and Routing 

### STEP 1) Create and Eloquent Model

```bash
php artisan make:model Movie
```

### STEP 2) Replace the code in Routes 

![image](https://user-images.githubusercontent.com/31894600/193736454-0d6ddfa6-5f42-475e-b4dd-d9f584513bb2.png)

Replace the existing routes with the following code

```bash
use App\Models\Movie;


Route::get('/movies', function () {
    return view('movies', [
        'title' => 'Movies',
        'movies' => Movie::all()
    ]);
});


Route::get('/movies/{id}', function ($id) {
    return view('movie', [
        
        'Movie' => Movie::find($id)
    ]);
});

```

### STEP 3) Add Moview data into the Database Seed

Open the DatabaseSeeder.php file

![image](https://user-images.githubusercontent.com/31894600/194681479-64d91d9f-18fd-420c-81a4-2def27c380b8.png)

Replace the code with the following 

```bash

<?php

namespace Database\Seeders;

use Illuminate\Database\Seeder;
use App\Models\Movie;

class DatabaseSeeder extends Seeder
{
    public function run()
    {

        Movie::create([
                'Title' => 'Scarface',
                'Year' => 1983,
                'Description' => 'Scarface (Caracortada, en Hispanoamérica; El precio del poder, en España) es una película     estadounidense de drama criminal de 1983 dirigida por Brian De Palma y escrita por Oliver Stone. Se trata de una nueva versión del filme del mismo nombre de 1932 y cuenta la historia del refugiado cubano Tony Montana (Al Pacino), que llega sin un centavo a Miami en la década de 1980 y se convierte en un poderoso narcotraficante. La película está coprotagonizada por Steven Bauer, Michelle Pfeiffer, Mary Elizabeth Mastrantonio y Robert Loggia.2​ De Palma dedicó esta versión de Scarface a los escritores de la película original, Howard Hawks y Ben Hecht.3​',
                'Genre' => 'Action',
                'Director' => 'Brian De Palma',
                'Producer' => 'Martin Bregman',
                'Actors' => 'Al Pacino'

            ]);
        Movie::create([
                'Title' => 'Avatar',
                'Year' => 2009,
                'Description' => 'Avatar (comercializada como Avatar de James Cameron) es una película épica de ciencia ficción militar estadounidense de 2009,6​7​ escrita, producida y dirigida por James Cameron y protagonizada por Sam Worthington, Zoe Saldaña, Sigourney Weaver, Stephen Lang y Michelle Rodriguez.

                 Está ambientada en el año 2154 y los acontecimientos que narra se desarrollan en Pandora, una luna (y aparentemente la más grande) de un planeta similar a Júpiter llamado Polífemo habitada por una especie humanoide llamada navi, con la que los humanos se encuentran en conflicto debido a que uno de sus clanes está asentado alrededor de un gigantesco árbol que cubre una inmensa veta de un mineral muy cotizado y que supondría la solución a los problemas energéticos de la Tierra: el unobtainium.8​9​ Jake Sully, un marine que quedó paralítico, es seleccionado para participar en el programa Avatar, un proyecto que transporta la mente de los científicos a unos cuerpos artificiales de navi para que la comunicación con los nativos resulte así más sencilla.10​ Durante esa búsqueda de confianza entre Jake y los navi, Jake debe ser aprobado por la tribu y experimenta todas las relaciones con el bosque, la fauna y la flora que tienen los nativos, junto con sus costumbres y su lengua. A pesar del fin científico del proyecto, el coronel Quaritch, quien dirige la defensa de la base humana en Pandora, convence a Jake para que le proporcione información sobre los nativos en caso de que fuera necesario recurrir a la fuerza para que se marchen. En un principio, Jake cumple profesionalmente su misión, pero se enamora de una de las nativas, Neytiri, y se da cuenta de que estos jamás renunciarán a su tierra, haciendo inevitable un conflicto armado; él deberá decidir de qué lado está.',
                'Genre' => 'Action',
                'Director' => 'James Cameron',
                'Producer' => 'James Cameron, Jon Landau',
                'Actors' => 'Sam Worthington, Zoe Saldana'
        ]);
        Movie::create([
                'Title' => 'Avengers',
                'Year' => 2012,
                'Description' => 'Marvel The Avengers4​ (titulada The Avengers: Los Vengadores en Hispanoamérica y Los Vengadores en España), o simplemente The Avengers, es una película de superhéroes estadounidense de 2012 basada en el equipo de superhéroes homónimo de Marvel Comics, producida por Marvel Studios y distribuida por Walt Disney Studios Motion Pictures, en colaboración con Paramount Pictures.N 1​ Es la sexta película del Universo cinematográfico de Marvel (UCM). La película fue escrita y dirigida por Joss Whedon, y cuenta con un reparto coral que incluye a Robert Downey Jr., Chris Evans, Mark Ruffalo, Chris Hemsworth, Scarlett Johansson y Jeremy Renner como el equipo titular, junto a Tom Hiddleston, Clark Gregg, Cobie Smulders, Stellan Skarsgård y Samuel L. Jackson. En The Avengers, Nick Fury, director de la agencia de espionaje S.H.I.E.L.D., recluta a Tony Stark, Steve Rogers, Bruce Banner, Thor, Natasha Romanoff y Clint Barton para formar un equipo que debe evitar que Loki, hermano de Thor, se apodere de la Tierra.',
                'Genre' => 'Action',
                'Director' => 'Joss Whedon                ',
                'Producer' => 'Kevin Feige',
                'Actors' => 'Robert Downey Jr., Chris Evans, Mark Ruffalo, Chris Hemsworth'
        ]);   
    }
}

```

### STEP 4) Run the Seed process

```php
php artisan db:seed
```

### STEP 5) Modify code in 'movies.blade.php' file

![image](https://user-images.githubusercontent.com/31894600/194682217-04ec4965-7332-4946-864f-25b021ac1701.png)

Replace all code with the following

```php
<h1>{{$title}}</h1>
@foreach($movies as $Movie)
<h2>
    <a href="/movies/{{$Movie['id']}}">
        {{$Movie['Title']}} - {{$Movie['Year']}}
    </a>
</h2>
<h3>
    Genre: {{$Movie['Genre']}}
</h3>
<h3>
    Director: {{$Movie['Director']}}
</h3>
<h3>
    Producer: {{$Movie['Producer']}}
</h3>
<p>
    {{$Movie['Description']}}
</p>

@endforeach
```
### STEP 6) Add a new view called 'movie.blade.php'

Add the following code

```php
<h1>{{$Movie['Tittle']}}</h1>
<h3>
    Genre: {{$Movie['Genre']}}
</h3>
<h3>
    Director: {{$Movie['Director']}}
</h3>
<h3>
    Producer: {{$Movie['Producer']}}
</h3>
<p>
    {{$Movie['Description']}}
</p>

```

### STEP 7) Open the app on your Browser

```bash
  php artisan serve
```

 http://127.0.0.1:8002/movies
 

![image](https://user-images.githubusercontent.com/31894600/194682349-6ede4c43-ad3f-4289-845e-c6dca6b49e84.png)
