# Git untuk Kolaborasi

## Pendahuluan

Selain untuk mengelola aset digital milik diri sendiri, kita bisa menggunakan Git untuk berkolaborasi dalam suatu repo di GitHub yang bisa diakses bersama. Dalam kasus seperti ini, berarti ada 2 peran:

1. Pemilik repo, sering disebut sebagai *upstream author*.
2. Kontributor, yaitu orang-orang yang akan berkontribusi memberikan konten.

Untuk situasi seperti ini, diasumsikan:

1. *Upstream author* telah membuat repo git di GitHub
2. Kontributor telah mengetahui adanya repo tersebut, tertarik untuk berkontribusi, sudah mengetahui apa yang akan diberikan ke proyek (repo GitHub *upstream author*) tersebut.
3. Pembahasan selanjutnya adalah tentang bagaimana kontributor bisa mengirimkan kontribusi ke repo GitHub milik *upstream author*.

Dalam pembahasan ini:

1. *Upstream author* adalah *pradiktaby*.
2. Kontributor adalah *febbyprasetyo*
3. Repo dari *upstream author* adalah **pradiktaby** yang bisa diakses di [https://github.com/Pradiktaby/collaboration](https://github.com/Pradiktaby/collaboration)

## Fork

Fork adalah membuat clone dari suatu repo di GitHub milik *upstream author*, diletakkan ke milik kontributor. Fork hanya dilakukan sekali saja. Pada dasarnya, proses untuk fork ini meliputi:

1. Fork repo di web GitHub.
2. Clone fork tersebut di komputer lokal.

Kontributor harus mem-*fork* repo *upstream author* sehingga di repo kontributor muncul repo tersebut. Proses *forking* ini dijelaskan dengan langkah-langkah berikut:

1. Login ke GitHub
2. Akses repo yang akan di-*fork*: https://github.com/Pradiktaby/collaboration
3. Pada sisi kanan atas, klik Fork:

![Capture52](https://user-images.githubusercontent.com/127824845/225033237-d6ce1722-9021-47b3-ab64-00fdd2a12699.PNG)

4. Pilih akan ditempatkan di account mana.

![Capture37](https://user-images.githubusercontent.com/127824845/225033155-ec2b98bd-a172-4be8-a7f4-725877abe8be.PNG)

5. Setelah proses, repo dari *upstream author* sudah berada di account GitHub kita (kontributor)

![Capture38](https://user-images.githubusercontent.com/127824845/225033161-cd9abe31-e526-4138-9a7a-7d6b7a1c7487.PNG)

Setelah proses tersebut, clone di komputer lokal :

![Capture39](https://user-images.githubusercontent.com/127824845/225033165-bb4a434c-3609-49dd-9cc0-c03aa806e51a.PNG)

Setelah itu, konfigurasikan repo lokal kontributor. Pada kondisi saat ini, di komputer lokal sudah terdapat repo `collaboration` yang berada pada direktori dengan nama yang sama. Untuk keperluan berkontribusi, ada 2 nama repo yang harus diatur:

  1. **origin**: menunjuk ke repo milik kontributor di GitHub, hasil dari fork.
  2. **upstream**: menunjuk ke repo milik *upstream* author (repo asli) di account *oldstager*.

Repo `origin` sudah dituliskan konfigurasinya pada saat melakukan proses clone dari repo kontributor. Konfigurasi repo *upstream* harus dibuat.

![Capture40](https://user-images.githubusercontent.com/127824845/225033170-6e70f6ab-8972-4849-b066-6be06959ac30.PNG)

## Mengirimkan Pull Request 

Setiap kali melakukan perubahan, kirim perubahan tersebut. Pengiriman ini disebut dengan *Pull Request*. Pada posisi ini, kontributor bisa mengirimkan kontribusi dengan cara mengirimkan *pull request* (PR) ke *upstream author*. Secara umum, langkah-langkahnya adalah sebagai berikut:

1. Kontributor akan bekerja di repo lokal (create, update, delete isi)
2. Commit
3. Push ke repo kontributor
4. Kirimkan PR ke repo *upstream author*.
5. *Upstream author* me-*review* dan kemudian menyetujui (*merge*) ke master atau menolak PR.
6. Jika disetujui dan di-*merge* ke repo master dari *upstream author*, sinkronkan repo di komputer lokal dan repo GitHub kontributor.

### Membuat Perubahan di Repo Lokal

Sebelum melakukan perubahan, pastikan:

1. Sudah ada koordinasi secara manual tentang perubahan-perubahan yang akan dilakukan.
2. Setelah melakukan perubahan-perubahan, pastikan bahwa isi repo lokal tersinkronisasi dengan repo dari *upstream author*.
3. Cara melakukan sinkronisasi:

![Capture41](https://user-images.githubusercontent.com/127824845/225033172-0c0c0ff5-3c3f-47f7-bef5-539ed4df295e.PNG)

4. Lakukan perubahan-perubahan, setelah itu push ke **origin** (milik kontributor)

![Capture42](https://user-images.githubusercontent.com/127824845/225033184-05a13504-8928-4563-9361-7b9cf9f46ff7.PNG)

![Capture43](https://user-images.githubusercontent.com/127824845/225033193-f55d578c-c70c-4692-bfb7-29639ba9cc67.PNG)

5. Setelah itu, buka halaman Web dari repo kontributor [https://github.com/Pradiktaby/collaboration](https://github.com/Pradiktaby/collaboration). Pada halaman tersebut akan ditampilkan isi yang kita push.

![Capture47](https://user-images.githubusercontent.com/127824845/225033208-4e4b435b-8ade-49d4-a86e-fe5172c61ba8.PNG)

6. Pilih ```Compare and pull request```, kemudian isikan deskripsi PR dan klik pada ```Create pull request```:

7. Pada repo *upstream author*, muncul angka 1 (artinya jumlahnya 1) pada ```Pull requests``` di bagian atas.

8. *Upstream author* bisa menyetujui setelah melakukan review : klik pada ```Pull requests```, akan muncul PR dengan message seperti yang ditulis oleh kontributor (*Add: contributor*). Klik pada PR tersebut, review kemudian klik ```Merge pull request``` diikuti dengan ```Confirm merge```. Setelah itu, status akan berubah menjadi ```Merged```.

![Capture48](https://user-images.githubusercontent.com/127824845/225033217-416ac415-6a40-4295-9565-5c1331c49cb3.PNG)

9. Sinkronkan semua repo (lokal maupun GitHub kontributor)

![Capture49](https://user-images.githubusercontent.com/127824845/225033223-412b2b3d-26a8-465c-a1b7-efa281bc489d.PNG)

![Capture50](https://user-images.githubusercontent.com/127824845/225033228-b583d4a1-4a90-4be3-95d0-81c63290200c.PNG)

![Capture51](https://user-images.githubusercontent.com/127824845/225033233-40f0b690-0cc9-4de8-8414-f600aefd6186.PNG)

## Konflik

Ada kemungkinan, jika satu orang mengirimkan PR untuk satu atau lebih file dan sementara itu ada lainnya juga yang mengirimkan PR pada satu atau lebih file yang sama, maka akan terjadi konflik karena ada satu atau lebih file yang **sama** yang di-edit dan akan di-*merge*. Jika sampai terjadi kasus seperti ini, maka *upatream author* **harus** menolak semua PR dan kemudian masing-masing kontributor diharapkan menyelesaikan secara manual (offline) kemudian memutuskan siapa yang akan mengirimkan PR.