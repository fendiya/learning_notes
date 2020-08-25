# what is it ? 
Jika DBMS Mysql punya SQL query untuk berinteraksi seperti select/update/delete ke DBMS engine. maka Laravel punya Tinker untuk berinteraksi dengan aplikasi. berinterkasi seperti membuat object, mengetest method/connection. 

## Tinker Test DB Connection
```php
vagrant@homestead:~/code/POS$ php artisan tinker
Psy Shell v0.10.4 (PHP 7.4.8 — cli) by Justin Hileman
`>>> DB::connection()->getPdo();
=> PDO {#3105
     inTransaction: false,
     attributes: {
       CASE: NATURAL,
       ERRMODE: EXCEPTION,
       AUTOCOMMIT: 1,
       PERSISTENT: false,
       DRIVER_NAME: "mysql",
       SERVER_INFO: "Uptime: 161673  Threads: 6  Questions: 190  Slow queries: 0  Opens: 270  Flush tables: 3  Open tables: 189  Queries per second avg: 0.001",
       ORACLE_NULLS: NATURAL,
       CLIENT_VERSION: "mysqlnd 7.4.8",
       SERVER_VERSION: "8.0.20-0ubuntu0.20.04.1",
       STATEMENT_CLASS: [
         "PDOStatement",
       ],
       EMULATE_PREPARES: 0,
       CONNECTION_STATUS: "192.168.10.10 via TCP/IP",
       DEFAULT_FETCH_MODE: BOTH,
     },
   }
```

## Tinker Test Select DB
```php
vagrant@homestead:~/code/POS$ php artisan tinker
>>> use App\EmployeePosition;
>>> EmployeePosition::all();
=> Illuminate\Database\Eloquent\Collection {#4047
     all: [
       App\EmployeePosition {#3800
         id: 1,
         position_name: "Store Administrator",
         created_at: null,
         updated_at: null,
       },
       App\EmployeePosition {#3432
         id: 2,
         position_name: "Store Administrator",
         created_at: "2020-08-25 13:29:33",
         updated_at: "2020-08-25 13:29:33",
       },
     ],
   }
>>> EmployeePosition::find(1);
=> App\EmployeePosition {#3115
     id: 1,
     position_name: "Store Administrator",
     created_at: null,
     updated_at: null,
   }
```
