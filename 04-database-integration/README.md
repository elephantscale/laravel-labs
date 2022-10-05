# Integrate MySQL into the Laravel Project

### STEP 1) Modify env file

Navigate to the env file in your Laravel project and add the MySQL connection information

![image](https://user-images.githubusercontent.com/31894600/193970845-de8c2905-f244-43a8-83fa-fc3ef40b4cab.png)

### STEP 2) Create Migration for the Movie entitiy

Run the following command

```bash
php artisan make:migration create_movies_table
```

The result of this command going to be a new file under the migrations folder

![image](https://user-images.githubusercontent.com/31894600/193975104-18097b8a-ff0c-4957-bc3a-a53c25b7b43c.png)

### STEP 3) Edit the created Migration file


Replace the up function with the following code

```php
 public function up()
    {
        Schema::create('movies', function (Blueprint $table) {
            $table->id();
            $table->string('Title');
            $table->string('Genre');
            $table->string('Director');
            $table->string('Producer');
            $table->string('Actors');
            $table->integer('Year');
            $table->longText('Description');
            $table->timestamps();
        });
    }
```
 ![image](https://user-images.githubusercontent.com/31894600/193976793-5385ce93-ce0f-4cf5-8a78-74b1661e93f1.png)

### STEP 4) Run the migration to create the table on MySQL

Run the following command

```bash
php artisan migrate
```

```bash
Output

   INFO  Preparing database.  

  Creating migration table .................................... 33ms DONE

   INFO  Running migrations.  

  2014_10_12_000000_create_users_table .................................... 63ms DONE
  2014_10_12_100000_create_password_resets_table .......................... 57ms DONE
  2019_08_19_000000_create_failed_jobs_table .............................. 54ms DONE
  2019_12_14_000001_create_personal_access_tokens_table ................... 103ms DONE
  2022_10_05_032541_create_movies_table ................................... 37ms DONE
```

