First init to existing repository and existing project, follow below : 
    1. cd <proyect folder>
    2. git init
    3. git remote add origin <link to repo> --> menambahkan remote repository ke local 
    4. git fetch origin --> mengambil perubahan yang ada di remote repo, tapi karena baru jadi kosong
    5. git checkout master --> pindah ke branch master (ini tidak dilakukan dari android studio)

    then  : 
    1. git add --all
    2. git commit -m "<message>"
    3. git push