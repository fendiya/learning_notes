# List Error Vagrant
--------------------------------------------

1.  **Description : Error ketika run command vagrant up untuk image laravel/homestead.**\
    **Error Message : Failed to attach the network LUN (VERR_INTNET_FLT_IF_NOT_FOUND)**\
    **Solusi :**\
        1. Double Klik, Host Only Virtual Box Adapter dari COntorl Panel>Network COnnection.\
        2. Disable NDIS6, lalu enable lagi,\
        3. Disable Host Only Virtual Box Adapter, lalu enable lagi\
        4. run kembali coomand vagrant up\

2.  **Description : Error ketika run command vagrant up untuk image laravel/homestead.**\
    **Error Message : Could not resolve host: vagrantcloud.com**\
    **Solusi :**\
        1. edit vagrantfile di folder homestead
        2. tambahkan parameter `config.vm.box_check_update = false` dibawah `Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|`