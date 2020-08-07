Vagrant adalah orchestration tools untuk virtual machine. kedudukannya sama seperti docker cli yang meng-orchestrate container. vagrant punya vagrantfile docker punya dockerfile.

jadi vagrant akan menjalankan vagrantfile dan mengambil image dari vagrant image repository. sama halnya dengan docker yang akan mengambil image dari docker hub repository atau private repository yang kita tentukan.

actuallnya ketika di jalankan, vagrant akan membuat guest os di virtual box/vmware lalu mengkonfigurasi osnya dan lainnya2 sesuai dengan config di vagrant file.

beberapa command vagrant : 

vagrant box add laravel/homestead
    # command diatas akan mendownload box (kalau di docker namanya image ) laravel/homestead dari public vagrant repository.

vagrant box list
    # command diatas akan melist box yang ada di lokal kita. 

vagrant run
    # command ini akan menstart guest os/box. jika boxnya blm ada di lokal atau kita belum menjalankan "box add" maka command ini akan menjalankan command "box add"

vagrant ssh
    # command ini sama dengan ssh ke dalam guest OS.

set VAGRANT_LOG=ERROR/INFO/DEBUG
vagrant run
    # command di atas akan men set error level untuk membantu melakukan troubleshooting.