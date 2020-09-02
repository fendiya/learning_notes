## simple array
artinya keynya adalah index 0,1,2,3, dll
```php
$menu = ['nasi goreng','somay','jus jambu'];

// cara mengkasesnya :
foreach ($arr as $val){
    echo ($val);
}
```

## custom key value
```php
// keynya yang harusnya index kita ubah jadi 'makanan' dan 'minuman' 
// dan tidak boleh ada 2 key yang sama dalam satu array 
// tidak boleh ada 'makanan'=>'bakso' dalam satu array, kalau mau buat array of array
$order = ['makanan'=>'nasi goreng','minuman'=>'jus jambu'];

// cara mengkasesnya :
foreach ($order as $cat => $nama){
    echo ('jenis pesanan :'+$cat+' nama pesanan :'+$nama);
}
```

## array of array custom key value
```php
$orders = [ ['makanan'=>'nasi goreng','minuman'=>'jus jambu'],
            ['makanan'=>'bakso','minuman'=>'air putih']];

// cara mengkasesnya :
foreach ($orders as $order)
    foreach ($order as $cat => $nama){
        echo ('jenis pesanan :'+$cat+' nama pesanan :'+$nama);
    }
}
```

## laravel collection of array
```php
$orders = collect ([ ['makanan'=>'nasi goreng','minuman'=>'jus jambu'],
                    ['makanan'=>'bakso','minuman'=>'air putih']]);

// cara mengkasesnya :
$orders->pluck('makanan');

//outputnya : 
nasi goreng
bakso
```