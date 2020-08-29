# Definisi : 
--------------------------------------------

Vagrant adalah orchestration tools untuk virtual machine. kedudukannya sama seperti docker cli yang meng-orchestrate container. vagrant punya vagrantfile docker punya dockerfile.

jadi vagrant akan menjalankan vagrantfile dan mengambil image dari vagrant image repository. sama halnya dengan docker yang akan mengambil image dari docker hub repository atau private repository yang kita tentukan.

actuallnya ketika di jalankan, vagrant akan membuat guest os di virtual box/vmware lalu mengkonfigurasi osnya dan lainnya2 sesuai dengan config di vagrant file.

# Beberapa command vagrant yang pernah saya gunakan. : 
--------------------------------------------

`vagrant box add laravel/homestead`
>command diatas akan mendownload box (kalau di docker namanya image ) laravel/homestead dari public vagrant repository.

`vagrant box list`
>command diatas akan melist box yang ada di lokal kita (kalau di docker namanya image list). 

`vagrant global-status`
>command diatas akan me list VM yang kita miliki beserta IDnya (kalau di docker namanya container list), ID ini bisa kita gunakan untuk men start VM tertentu dengan command `vagrant up id`

`vagrant up`
>command ini akan menstart guest os/box. jika boxnya blm ada di lokal atau kita belum menjalankan "box add" maka command ini akan menjalankan command "box add" secara otomatis.

`vagrant ssh`
>command ini sama dengan ssh ke dalam guest OS. untuk mencari detail environemnt variable yang digunakan untuk ssh gunakan command `vagrant ssh-config`.

`set VAGRANT_LOG=ERROR/INFO/DEBUG`
`vagrant run / another command`
>command di atas akan men set error level untuk membantu melakukan troubleshooting.

`vagrant halt`
>command ini akan menshutdown guest OS. untuk start lagi pakai vagrant up

`vagrant suspend`
>command ini akan mensuspend guest OS seperti hibernate tapi lebih cepat ketika mau menlanjutkan kerjaan. menyalakan kembali dengan command vagrant resume.

`vagrant reload --provision` / `vagrant provision (box id)`
>gunakan command ini ketika ada perubahan di provision script, contoh kita melakukan perubahan mapping folder di file Homestead.yaml milik laravel (mapping file di file yaml ini maksudnya ingin menambahkan sharing folder di guestOS), maka untuk mereloadnya gunakan command ini. command ini akan merestart guest OS dan mengeksekusi kembali provision script kita (contohnya ingin mereload yaml file).

## Start Vagrant without internet
jika kita mendapat error ketika run vagrant up karena tidak ada internet, maka itu berarti vagrant box kita kita di set untuk selalu mengecek update ke suatu alamat contohnya adalah box laravel/homestead yang akan selalu melihat update ke vagrantcloud.com. salah satu cara agar vagrant tidak mengecek update adalah mendisable check update di vagrantfile, menambahkan parater `config.vm.box_check_update = false`, defaut valuenya adalah true. contoh seperti dibawah. \

Sebelumnya : \
```vagrantfile
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|      
    if File.exist? aliasesPath then
        config.vm.provision "file", source: aliasesPath, destination: "/tmp/bash_aliases"
        config.vm.provision "shell" do |s|
            s.inline = "awk '{ sub(\"\r$\", \"\"); print }' /tmp/bash_aliases > /home/vagrant/.bash_aliases && chown vagrant:vagrant /home/vagrant/.bash_aliases"
        end
    end
```

Setelah di ubah : \
```vagrantfile
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

    config.vm.box_check_update = false
    
    if File.exist? aliasesPath then
        config.vm.provision "file", source: aliasesPath, destination: "/tmp/bash_aliases"
        config.vm.provision "shell" do |s|
            s.inline = "awk '{ sub(\"\r$\", \"\"); print }' /tmp/bash_aliases > /home/vagrant/.bash_aliases && chown vagrant:vagrant /home/vagrant/.bash_aliases"
        end
    end
```