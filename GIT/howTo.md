### First init to existing repository and existing project, follow below : 
    1. cd <proyect folder>
    2. git init
    3. git remote add origin <link to repo> --> menambahkan remote repository ke local 
    4. git fetch origin --> mengambil perubahan yang ada di remote repo, tapi karena baru jadi kosong
    5. git checkout master --> pindah ke branch master (ini tidak dilakukan dari android studio)

    then  : 
    1. git add --all
    2. git commit -m "<message>"
    3. git push.

### add local changed file to remote repository
1. `git add <filnename>` 
2. To check whether our files has been added use comman `git status --porcelain | findstr "^A"`
3. then commit our changes using command `git commit -m "message"`
4. To check  list of commit has been done in our local use command `git log`. 
    (HEAD -> master) means already in local master branch not not yet in remote master branch. 
    (origin/master) means already pushed to remote repository.
    To check list of files in one commit object use comand `git diff-tree --no-commit-id --name-only -r <commit id>`
