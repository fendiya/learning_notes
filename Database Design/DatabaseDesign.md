# Design OLTP Database
Use normalization : \
Why : to prevent data duplication (database size) and performance optimization during Insert, Update or Delete.

## 1. 1st Level Normalisation Rule \
    1. Setiap kolom hanya berisikan satu data contohnya (bakso), tidak boleh seperti (bakso,gado-gado,es teler)
    2. setiap kolom berisikan data yang memiliki tipedata dan format yang sama. contohnya kalau kolom tgl lahir isinya (1 Januri 2001), maka tidak boleh ada value yang isinya (1 Kliwon bulan sura tahun 2001). \
    3. Nama kolom tidak boleh sama dalam satu table. \
    4. Urutan data tersimpan tidak masalah, gunakan fungsi order by di SQL untuk mengurutkan hasil data. \

## 2. 2nd Level Normalization Rule\
    Ketika table kita menggunakan composite key, tidak boleh ada kolom yang hanya bergantung pada satu key. Solusinya adalah dengan memecah table tersebut menjadi 2 table. Contoh: 

    `Table : Student_Score`
    |Student_ID|Subject_ID|Score|Teacher_Name|
    |----------|----------|-----|------------|
    |1|a1|100|fendi|
    |2|a1|100|fendi|
    |1|a2|100|Awan|

    Table diatas memiliki composite Key yaitu student_id dan subject_id. yang bermasalah adalah kolom teacher_name, karena subject yang sama diajarkan oleh guru yang sama, artinya kolom techer_name hanya dependent dengan kolom subject_id dan tidak dengan student_id, maka lebih baik di pisah jadi 2 table seperti dibawah.\
    Masalah akan kita rasakan ketika misal ada perubah teacher_name dari fendi menjadi fendiy, maka akan ada 2 row yang harus di update (data duplication making more task/performace degradation). tapi dengan solusi dibawah hanya perlu satu row yang di update. \

    `Table : Student_Score`
    |Student_ID|Subject_ID|Score|
    |----------|----------|-----|
    |1|a1|100|
    |2|a1|100|
    |1|a2|100|

    `Table : Subject`
    |Subject_ID|Subject_Name|Teacher_Name|
    |----------|------------|------------|
    |a1|java|fendi|
    |a2|php|awan|

## 3. 3rd Level Normalization Rule \
    Ketika menggunakan primary key, dan ada data yang tidak dependent ke primary kay tapi dependent key kolum lainnya. maka lebih baik di buat jadi 2 table. Contoh : 

    `Table : Student_Score`
     |Score_id|Student_ID|Subject_ID|Score|Exam_Tipe|Bobot_Nilai|
     |--------|----------|----------|-----|---------|-----------|
     |1|1|a1|100|Teori|40|
     |2|2|a1|100|Teori|40|
     |3|1|a1|100|Praktik|60|

     Table diatas menunjukkan bobot nilai praktek 60 dan bobot nilai teori 40. jadi kolom bobot_nilai hanya dependent ke table Exam_tipe bukan score_id. solusinya seperti dibawah.

     `Table : Student_Score`
     |Score_id|Student_ID|Subject_ID|Score|Exam_id|
     |--------|----------|----------|-----|---------|
     |1|1|a1|100|1|
     |2|2|a1|100|1|
     |3|1|a1|100|2|

     `Table : Subject_exam`
     |Exam_id|Exam_Type|Bobot_Nilai|
     |--------|----------|---------|
     |1|Teori|40|
     |2|Praktik|60|
     
## 4. 3.5th/BNCF Level Normalization Rule\
    Jika dalam satu table memiliki 2 kandidat composite key, maka labih baik di pisahkan jadi 2 table. Contoh : 

    `Table : Student`
    |Student_ID|Subject_ID|Teacher_Name|
    |----------|----------|------------|
    |1|a1|fendi|
    |2|a1|awan|

    Kondisi yang di inginkan adalah satu subject bisa di ajarkan oleh teacher yang berbeda. dan table diatas memiliki composite key yaitu student_id dan Subject_id. tapi ada kandidat composite key yang lain yaitu subject_id dan techer_name. solusinya adalah dengan memecah menjadi 2 table yaitu : 

     `Table : Student`
    |Student_ID|Teacher_ID|
    |----------|----------|
    |1|t1|
    |2|t2|

     `Table : Teacher`
    |Teacher_ID|Subject_ID|Teacher_Name|
    |----------|----------|------------|
    |t1|a1|fendi|
    |t2|a1|awan|

## Jenis Key Dalam Table
What is Key : Key adalah kolom yang bisa digunakan untuk membedakan satu row/data dengan data yang lainnya. ada 3 jenis key: \
1. Primary key --> Ada Satu Kolom yang dapat membedakan setiap row.\
    |Table Name | Student|
    |-----------|--------|
    |Column | Student_id, Student_name, Student_address|
    |Primary Key | Student_id|

2. Composite Key --> Karena ada lebih dari satu/Dua atau lebih Kolom yang dapat membedakan setiap row.\
    |Table Name | Student_Score|
    |-----------|--------------|
    |Column | Student_Id, Subject_ID, Score|
    |Composite Key | Student_ID dan Subject_ID, kalau di table ini ada column Score_ID, maka Score_ID adalah primary key|

3. Secondary Key --> Kolom yang datanya unique tapi tidak bisa dijadikan primary atau composite key.