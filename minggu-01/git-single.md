# Instalasi Git

### Windows
Silahkan buka website resminya Git ( git-scm.com). Kemudian unduh Git sesuai dengan arsitektur komputer kita. Kalau menggunakan 64bit, unduh yang 64bit. Begitu juga kalau menggunakan 32bit. Sebelum install Git di Windows, anda harus sudah mempunyai editor teks yang didukung oleh Windws. Editor yang bisa dipilih banyak, tetapi disarankan menggunakan [Notepad++](https://notepad-plus-plus.org/) atau [Visual Studion Code](https://code.visualstudio.com/) atau [Vim](https://www.vim.org/). 

1. Setelah download Git, Silahkan klik dua kali file instaler Git yang sudah diunduh.. Klik **Next** untuk lanjut.

![01](https://user-images.githubusercontent.com/122883189/224073132-2738192d-de0f-41c0-bff0-2a9181181ace.PNG)

2. Selanjutnya menentukan lokasi instalasi. Biarkan saja apa adanya, kemudian klik **Next**

![02](https://user-images.githubusercontent.com/122883189/224073412-5b793c9d-085b-4eb1-8ac2-6c1957be1b6d.PNG)

3. Selanjutnya pemilihan komoponen. Tidak perlu diubah-ubah, sesuai dengan default saja. Klik pada **Next**.

![3](https://user-images.githubusercontent.com/122883189/224073451-81f57667-583a-46b3-9a10-9e8d52ffb403.PNG)

4. Selanjutnya pemlilihan direktori start menu, kemudian klik **NEXT**

![04](https://user-images.githubusercontent.com/122883189/224073488-61c942e9-e142-41c8-a11d-c8cdee98efae.PNG)

5. Pilih editor yang akan digunakan bersama dengan Git. Pada pilihan ini, digunakan Notepad++.

![05](https://user-images.githubusercontent.com/122883189/224073542-c507cb8e-8d76-4ac0-90b5-ad7e2f859b9a.PNG)

6. Selanjutnya pengaturan PATH Environment. Pilih yang tengah agar perintah git dapat di kenali di Command Prompt (CMD). kemudian klik **NEXT**

![Capture6](https://user-images.githubusercontent.com/122883189/224073581-361ce678-98e3-41f7-8a05-08163a454345.PNG)

7. Pilih OpenSSL untuk HTTPS. Git menggunakan https untuk akes ke repo GitHub atau repo-repo lain (GitLab, Assembla).

![Capture7](https://user-images.githubusercontent.com/122883189/224073638-535711b9-cf95-4cb2-9019-a94900f970c4.PNG)

8. Selanjutnya konversi line ending. Biarkan saja seperti ini, kemudian klik **Next**

![Capture8](https://user-images.githubusercontent.com/122883189/224073768-f3bcb5e9-3961-4384-a06d-13a0fdff5f58.PNG)

9. Selanjutnya pemilihan emulator terminal. Pilih saja yang bawah, kemudian klik **Next**

![Capture9](https://user-images.githubusercontent.com/122883189/224073806-c9ec1b46-f22a-4309-b14e-a0e3944c5a74.PNG)

10. Selanjutnya pemilihan opsi ekstra. Klik saja **Next**

![Capture10](https://user-images.githubusercontent.com/122883189/224073852-e7cbf1cc-d8bb-4cd1-82dc-bd21f0a85c3d.PNG)

11. Setelah itu proses instalasi akan dilakukan.

![Capture11](https://user-images.githubusercontent.com/122883189/224073909-fc99dd07-0f07-4f27-832f-64abe75c461b.PNG)

12. Setelah selesai, Klik pada **Finish**.

![Capture12](https://user-images.githubusercontent.com/122883189/224073992-1fe9b4c8-1c16-4af0-ab6a-ffe6e75329e9.PNG)

13. Tampilan jika akan menggunakan "Git Bash"

![Capture13](https://user-images.githubusercontent.com/122883189/224074044-baceb693-bd71-4292-aeed-cc16a063cdc0.PNG)

15. Tampilan jika akan menggunakan "Git GUI"

![Capture14](https://user-images.githubusercontent.com/122883189/224074083-71da5890-ec78-4afb-9cf9-fac6220c60cc.PNG)

16. Untuk mencoba dari command prompt, masuk ke command prompt, setelah itu eksekusi "git --version" untuk melihat apakah sudah terinstall atau belum. Jika sudah terinstall dengan benar, makan akan muncul hasil berikut:

![Capture15](https://user-images.githubusercontent.com/122883189/224074142-e8c760c6-dc27-4ed9-8ad5-779275d0111e.PNG)


# Konfigurasi Git

Untuk sistem operasi Windows, konfigurasi ini akan disimpan di ***C:\Document and Settings\NamaUser*** dengan nama file ***.gitconfig.*** Secara minimal, ada 2 hal yang perlu dikonfigurasi yaitu username dan email. Gunakan perintah berikut:

```
$ git config --global user.name "Nama Anda di GitHub"
$ git config --global user.email email@domain.tld
```
Isian di atas harus disesuaikan dengan nama serta email yang digunakan untuk mendaftar di GitHub. Untuk melihat konfigurasi yang sudah ada:

```
$ git config --list
user.email=phylossophie@gmail.com
user.name=Bambang Purnomosidi D. P.
color.ui=true
$
```

![Capture16](https://user-images.githubusercontent.com/122883189/224083982-4ef62a87-1c0c-4a84-9c33-76fbceb1b9e3.PNG)

# Mengelola Repo Sendiri di Account Sendiri

## Membuat Repo

Untuk membuat repo, gunakan langkah-langkan berikut:
1.  Klik tanda **+** pada bagian atas setelah login, pilih **New repository**

![Capture17](https://user-images.githubusercontent.com/122883189/224199813-ad9c8fb3-d84f-42a5-b381-43261ff63543.PNG)

2. Isikan nama, keterangan, serta lisensi. Jika dikehendaki, bisa membuat repo **Private**

![Capture18](https://user-images.githubusercontent.com/122883189/224199834-85b75a77-117f-4cc0-ab6c-204394557b22.PNG)

3. Klik ```Create Repository```
Setelah langkah-langkah tersebut, repo akan dibuat dan bisa diakses menggunakan pola ```https://github.com/username/reponame```. Pada repo tersebut, hanya akan muncul 1 file, yaitu LICENSE. Jika memilih membuat README pada saat langkah ke 2, juga akan muncul README.md. Ada atau tidak ada README.md tidak mempunyai efek apapun pada langkah ini.

## Clone Repo
Proses ```clone``` adalah proses untuk menduplikasikan remote repo di GitHub ke komputer lokal. Untuk melakukan proses ```clone```, gunakan perintah berikut:

![Capture21](https://user-images.githubusercontent.com/122883189/224867792-62a01fe7-a44d-4e65-ac9e-eb4c52f2c08b.PNG)

Setelah perintah ini, di direktori ```tekn-cloud-computing``` akan disimpan isi repo yang sama dengan di GitHub. Perbedaannya, di komputer lokal terdapat direktori ```.git``` yang digunakan secara internal oleh Git.

# Mengelola Repo

### Mengubah Isi - Push Tanpa Branching dan Merging

Perubahan isi bisa terjadi karena satu atau kombinasi beberapa hal berikut:
1. File dihapus
2. File diedit
3. Membuat file / direktori baru
4. Menghapus direktori

Untuk kasus-kasus tersebut, lakukan perubahan di komputer lokal, setelah itu push ke repo. 

![Capture22](https://user-images.githubusercontent.com/122883189/224867812-303360a9-6aa6-445b-a81b-619de30d868b.PNG)

![Capture23](https://user-images.githubusercontent.com/122883189/224867833-10fc9cd6-710c-4d16-b6a3-163b2fd9290b.PNG)

### Mengubah Isi dengan Branching and Merging

Secara umum, langkahnya adalah sebagai berikut:
1. Buat branch untuk menampung perubahan-perubahan
2. Lakukan perubahan-perubahan
3. Add dan commit perubahan-perubahan tersebut ke branch
4. Kembali ke repo master
5. Buat pull request di GitHub
6. Merge pull request di GitHub
7. Merge branch untuk menampung perubahan-perubahan tersebut ke master.
8. Selesai.

![Capture24](https://user-images.githubusercontent.com/122883189/224867855-561aa2c3-832b-416e-9ad9-b4769f531afb.PNG)

### Membuat Pull Request Kemduian Merge Pull

Setelah itu, kirim pull request (PR):

![Capture25](https://user-images.githubusercontent.com/122883189/224867872-a1943515-541b-4daf-a56d-b88944603bbb.PNG)

![Capture26](https://user-images.githubusercontent.com/122883189/224867896-7db0867d-e987-4a11-a234-a3718da11a73.PNG)

![Capture27](https://user-images.githubusercontent.com/122883189/224867929-398e1928-7a87-4dd0-b06d-653f30ef4c61.PNG)

![Capture28](https://user-images.githubusercontent.com/122883189/224867960-116b178b-2367-4599-a5a6-43983e64cca5.PNG)

![Capture29](https://user-images.githubusercontent.com/122883189/224867984-a7423fa6-6003-4229-babb-5ec6edb13e5a.PNG)

### Sinkronisasi

Suatu saat, bisa saja terjadi kita menggunakan komputer lain dan mengedit repo melalui repo lokal di komputer lain, setelah itu pindah ke kamputer lain lagi. Saat itu, kita perlu melakukan sinkronisasi ke kemputer lokal. Perintah untuk sinkronisasi adalah:

![Capture30](https://user-images.githubusercontent.com/122883189/224868008-262b203e-b06b-4fbf-a30e-766a296de4eb.PNG)

### Membatalkan Perubahan

![Capture31](https://user-images.githubusercontent.com/122883189/224868027-2bfcf62b-152f-48af-9da9-4ae3b4ead2a0.PNG)

### Undo Commit Terakhir

Suatu saat, mungkin ketika sudah terlanjur mem-*push* perubahan ke repo GitHub, setelah itu baru menyadari bahwa perubahan tersebut salah. Untuk itu, kita bisa melakukan ```git revert```.

![Capture32](https://user-images.githubusercontent.com/122883189/224868055-888ffe25-6379-418f-9fb3-5d39019c5b5a.PNG)

![Capture33](https://user-images.githubusercontent.com/122883189/224868067-f1d94ddf-60fa-47d4-98c8-ea2ae463e293.PNG)

Contoh di atas adalah contoh untuk mengubah README.md dengan beberapa commit. 





