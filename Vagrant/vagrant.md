# Definisi : 
--------------------------------------------

Vagrant adalah orchestration tools untuk virtual machine. kedudukannya sama seperti docker cli yang meng-orchestrate container. vagrant punya vagrantfile docker punya dockerfile.

jadi vagrant akan menjalankan vagrantfile dan mengambil image dari vagrant image repository. sama halnya dengan docker yang akan mengambil image dari docker hub repository atau private repository yang kita tentukan.

actuallnya ketika di jalankan, vagrant akan membuat guest os di virtual box/vmware lalu mengkonfigurasi osnya dan lainnya2 sesuai dengan config di vagrant file.

# Beberapa command vagrant yang pernah saya gunakan. : 
--------------------------------------------

vagrant box add laravel/homestead
>command diatas akan mendownload box (kalau di docker namanya image ) laravel/homestead dari public vagrant repository.

`vagrant box list`
command diatas akan melist box yang ada di lokal kita. 

`vagrant up`
command ini akan menstart guest os/box. jika boxnya blm ada di lokal atau kita belum menjalankan "box add" maka command ini akan menjalankan command "box add"

`vagrant ssh`
command ini sama dengan ssh ke dalam guest OS.

`set VAGRANT_LOG=ERROR/INFO/DEBUG`
`vagrant run / another command`
command di atas akan men set error level untuk membantu melakukan troubleshooting.

`vagrant halt`
command ini akan menshutdown guest OS. untuk start lagi pakai vagrant up

`vagrant suspend`
command ini akan mensuspend guest OS tapi lebih cepat ketika mau menlanjutkan kerjaan. menyelakan kembali dengan command vagrant resume.

`vagrant reload --provision`
gunakan command ini ketika ada perubahan di provision script, contoh kita melakukan perubahan mapping folder di file Homestead.yaml milik laravel, maka untuk mereloadnya gunakan command ini. command ini akan merestart guest OS dan mengeksekusi kembali provision script kita.