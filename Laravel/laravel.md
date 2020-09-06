### Features : 
- Blade : this is templating engine for building UI
- Component : UI component that can be used to standarize our UI object like input, button, form, panel, etc.
- Traits : it is like library/helper/util class, it can be used anywhere.
- Eloquent : ORM 
- Logging : it used Monolog, can have multiple handler dan formatter.
- DB Migration : can be used to build/drop table in database
- DB Seeder/Factory : can be used to seed dummy data or staic data for testing
- 


### Setup HomeStead
1. Install Vagrant\
2. Install VirtualBox\
3. Add Homestead Box to Local Laptop Repository. In other senctence it is same by saying "Download VIrtual Machine Template/Image from vagrant public repository to Local Laptop". do this by running command `vagrant box add laravel\homestead`\
4. Generate SSH KeyGen\
5. Edit Homestead.yaml\
6. Launch by running `vagrant up`\

### VSCODE Extension
1. PHP intelephense
2. php namespace resolver --> to help class namespace import


### Create New Project
1. Go to homestead environment. can use command `vagrant ssh`\
2. Go to root folder of Projects. Depend on configuration in yaml, find configuration for Folders->To in homestead.yaml, usualli it set to /home/vagrant/code. `cd /home/vagrant/code`\
3. run `laravel new <appname>`\


### PHP Artisan Command
#### Create Model/ORM
`php artisan make:model <ModelName> -m -s` 

What will Happen : \
1. it will create file app/ModelName.php
2. -m will 
    1. create file in database/migrations/xxx_ModelName_table.php and 
    2. will modify file in vendor/composer/autoload_classmap.php, by adding this record : App\\ModelName' => $baseDir . '/app/ModelName.php',
3. -s will 
    1. create file in database/seeds/ModelNameSeeder.php and 
    2. will modify file in in vendor/composer/autoload_classmap.php, by adding this record : 'ModelNameSeeder' => $baseDir . '/database/seeds/ModelNameSeeder.php'

Convention : 
1. Model name should in PascalCase (Captial in each first Word) ex:ModelName but in database should in snakecase all should be lowercase and separtated by underscore ex: model_name
2. Model Name should in singlular form (Employee) but in database it should be in plural form (Employees).
3. column name in model and in database should be in snake case or all lower and separated by underscore ex:employee_name.
4. column id in model and in database should be named as id without table name wrong sample : employee_id, right sample : id.

##### Migration
Laravel Migration will modify our database objectes. it has 2 methods, up and down. up will be called by using command `php artisan migrate` and down will be called using command `php artisan migrate:rollback`

##### Seeder
Laravel seeder digunakan untuk menginsert data/membuat data dummy di table kita sebanyak data yang kita buat di file seeder. Jika ada 5 data yang kita buat maka akan ada 5 rows di DB. tapi jika command seeder `php artisan db:seed` dijalankan 2 kali maka akan ada 10 data.\

secara default command db:seed hanya akan melihat isi file DatabaseSeeder.php, sehingga kita harus mendaftarkan file seeder kita ke file tersebut dengan menambahkan command `$this->call(EmployeePositionSeeder::class);`

jika butuh membuat banyak data dummy kita bisa menggunakan laravel model factories, sama seperti mengenerate lorem ipsum.

```php
 DB::table('employee_positions')->insert([
            'position_name'=>'Store Administrator',
            'created_at' => Carbon::now()->format('Y-m-d H:i:s'),
            'updated_at' => Carbon::now()->format('Y-m-d H:i:s')
            ]);
```

##### Factories
Laravel Factories digunakan untuk mengenerate data dummy untuk database kita, untuk membuatnya gunakan command. \
`php artisan make:factory -m EmployeePosition EmployeePositionFactory`
command diatas akan menggenerate 1 file di database/factories/EmployeePositionFactory.php.\

untuk mengenerate data dummy kita gunakan command yang sama dengan seeder yaitu `php artisan db;seed`, tapi sebelumnya kita harus me register factory file kita ke seeder filenya dengan cara mengedit seeder file dan menambahkan command `factory(EmployeePosition::class,10)->create();` artinya akan mengenerate 10 rows dummy data.

```php
factory(EmployeePosition::class,10)->create()->each(function ($positions){
         $positions->employees()->saveMany(factory(Employee::class,5)->make());
        });
```

#### Re generate autoload files
ketika membuat migration/seeder maka laravel akan membuat file dan juga mengedit autoload file yang terdapat pada path vendor/composer/autoload_classmap.php. file ini bisa kita regenerate dengan command `composer dump-autoload`. maka composer akan melihat configurasi autoload/classmap yang ada di file composer.json. 