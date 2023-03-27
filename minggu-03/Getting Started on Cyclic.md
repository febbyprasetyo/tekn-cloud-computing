# Deploy some code

1. Untuk memulai, buat sebuah direktori bernama **helloworld** di mesin lokal Anda.

2. Buka **Visual Studio Kode** dan Buka folder **"helloworld**" yang telah dibuat sebelumnya.

3. Langkah pertama adalah membuat file **server.js** di folder helloworld dengan mengklik kanan di bawah HELLOWORLD di panel Explorer dan memilih "file baru", atau dengan mengklik ikon file baru di sebelah HELLOWORLD. Beri nama file ini **server.js**.

4. Selanjutnya, masuk ke "terminal" Visual Studio Code. Untuk membukanya, gunakan pintasan keyboard (ctrl + `) atau pilih "View" -> "integrated terminal" dari menu paling atas.

5. Di terminal ketik perintah **npm init**.

6. Ini akan membuat file package.json di bawah folder helloworld.

![7](https://user-images.githubusercontent.com/122883189/227852254-27e467fe-84f6-40ac-95c5-8d7cfd09fe34.PNG)

7. Selanjutnya, Anda harus mengambil modul **express** menggunakan npm. Jalankan perintah berikut dari dalam terminal: **npm install express**. ini akan membuat folder **node_modules** dengan modul express baru serta memperbarui file **package.json** kita dengan dependensi

8. Selanjutnya mengedit file server.js Anda . Masukkan kode berikut:

![8](https://user-images.githubusercontent.com/122883189/227853714-bc730a26-5cc9-4b49-89cc-493706214ff9.PNG)
Pastikan file telah disimpan sebelum melanjutkan.

9. Selanjutnya, buat file bernama .gitignore yang berisi teks:

```
node_modules
```

10. Terakhir, keluarkan perintah berikut dari terminal terintegrasi: **git ini**t - ini akan menginisialisasi repositori git lokal di folder helloworld yang telah dibuat.

# Buat Repositori Github

1. Masuk ke akun Github Anda.

2. Temukan dan klik tombol "+" di Bilah Navigasi. Kemudian, pilih **"New Repository"** dari menu dropdown.

![9](https://user-images.githubusercontent.com/122883189/227854991-382a4e0c-10e1-41b5-b91b-b1b3713494c1.PNG)

3. Isi bidang teks nama repositori dengan nama proyek Anda. Pastikan juga bahwa opsi "Pribadi" dipilih:

![1](https://user-images.githubusercontent.com/122883189/227855209-3c3916be-2252-4bc7-9169-987dd4982e55.PNG)

4. Setelah itu, tekan tombol **"Create repository""**

# Hubungkan Repositori Git Lokal ke GitHub

1. Pertama, buka repositori GitHub Anda yang baru dibuat dan klik tombol "salin" di blok "Pengaturan Cepat":

![10](https://user-images.githubusercontent.com/122883189/227855750-4a71f13a-090a-406c-868c-48f684c292e9.PNG)
Ini akan menyalin URL repositori GitHub jarak jauh Anda.

2. Selanjutnya, kembali ke Terminal Anda lagi dan tambahkan URL jarak jauh ini dengan menjalankan perintah berikut:
```
git remote add origin URL
```

![11](https://user-images.githubusercontent.com/122883189/227856583-2148ab28-2e3c-4d42-b893-e3edecaba051.PNG)

# Hubungkan Repositori GitHub ke Cyclic

1. Daftar: https://app.cyclic.sh/api/login

![Capture1](https://user-images.githubusercontent.com/122883189/227857957-98613ceb-59b0-421c-a42d-653ca49287c4.PNG)

2. Menggunakan github sebagai login Anda

![Capture2](https://user-images.githubusercontent.com/122883189/227857856-d1d50df6-519a-4d4c-a900-0d0885e211cc.PNG)

3. Setelah Anda masuk, klik tombol hijau "Deploy" di bagian "Buat Aplikasi Baru":

![12](https://user-images.githubusercontent.com/122883189/227861086-0224a631-2e9d-47b7-8bef-a2dc59c2f6ec.PNG)

4. Di bagian atas halaman, alihkan ke tab **"Link Your Own"** dan mulailah mengetik nama repositori GitHub pribadi Anda yang menghosting kode Anda (dalam hal ini "helloworld")

![Capture9](https://user-images.githubusercontent.com/122883189/227861763-379de8a4-0df5-4710-bd04-513674224310.PNG)

5. Saat diminta, Anda perlu mengonfirmasi akses Github Anda, dan setelah mengonfirmasi, yang harus Anda lakukan hanyalah menyetujui dan menginstal.

![3](https://user-images.githubusercontent.com/122883189/227863793-3ccc5dc0-76ba-4bab-aae0-26604fb42d71.PNG)

6. Setelah Anda menyetujui dan menginstal, proses penerapan akan dimulai dalam 2–3 menit.

![13](https://user-images.githubusercontent.com/122883189/227864306-06227236-ca03-4d19-9db3-7faa95ae35d1.PNG)
Konfirmasikan akses ke repositori dengan sekali lagi memasukkan kata sandi GitHub Anda.

7. Kode Anda sekarang akan membutuhkan waktu untuk dibuat. Setelah selesai, Anda akan melihat beberapa confetti dan teks "You're Live!" di bawah log build. Dari sini Anda dapat mengeklik tombol "Buka Dasbor" untuk melihat informasi tentang aplikasi yang diterapkan, termasuk tautan yang dibuat untuk melihatnya secara langsung!
