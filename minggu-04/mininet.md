# Panduan Mininet di Ubuntu

## Langkah 1: Instal

Login, instal net-tools, git clone dan instal Mininet di sistem Ubuntu Anda.

```
feby@feby-VirtualBox:~$ sudo apt-get install net-tools
feby@feby-VirtualBox:~$ git clone https://github.com/mininet/mininet
feby@feby-VirtualBox:~$ mininet/util/install.sh -w
feby@feby-VirtualBox:~$ mininet/util/install.sh -a
```

Tunggu sampai penginstalan selesai.

## Langkah 2: Topologi Minimal

Mulai topologi minimal dan masukkan CLI:

![11](https://user-images.githubusercontent.com/122883189/231036557-fea0b562-f4bb-440e-b62c-6ee40e522865.PNG)

Topologi default adalah topologi minimal, yang mencakup satu switch kernel OpenFlow yang terhubung ke dua host, ditambah pengontrol referensi OpenFlow.

## Langkah 3: Berinteraksi dengan Host dan Switch

Tampilkan perintah CLI Mininet:

```
mininet> help
```

![12](https://user-images.githubusercontent.com/122883189/231037006-949edbd9-35cf-43ae-8939-c6f7143d344e.PNG)

node tampilan:

```
mininet> nodes
```

![13](https://user-images.githubusercontent.com/122883189/231037380-c79fa71c-dbbe-4b16-8046-8446270d1b54.PNG)

Tampilkan tautan:

```
mininet> net
```

![14](https://user-images.githubusercontent.com/122883189/231037688-6a0474e2-daa2-4080-b0b0-ebd2a7d2be5d.PNG)

Membuang informasi tentang semua node:

```
mininet> dump
```

![15](https://user-images.githubusercontent.com/122883189/231037918-cc96565b-09d0-48d3-883d-566a7744bd74.PNG)

Anda akan melihat sakelar dan dua host terdaftar.

Jika string pertama yang diketik ke dalam Mininet CLI adalah nama host, switch atau controller, perintah dijalankan pada node tersebut. Jalankan perintah pada proses host:

```
mininet> h1 ifconfig -a
```

![16](https://user-images.githubusercontent.com/122883189/231038355-a2426fd1-02d6-4f51-95ea-f03e201ef33a.PNG)

Sebaliknya, switch secara default berjalan di namespace jaringan root, jadi menjalankan perintah pada "switch" sama dengan menjalankannya dari terminal biasa:

```
mininet> s1 ifconfig -a
```

![18](https://user-images.githubusercontent.com/122883189/231038703-b19bc53e-531f-4489-8215-05e7844ec959.PNG)

Perhatikan bahwa hanya jaringan yang divirtualisasi; Setiap proses host melihat serangkaian proses dan direktori yang sama. Misalnya, cetak daftar proses dari proses host:

```
mininet> h1 ps -a
```

![19](https://user-images.githubusercontent.com/122883189/231038950-91f1dd90-8b17-4562-9fb0-57399308c95a.PNG)

Ini harus sama persis dengan yang dilihat oleh namespace jaringan root:

```
Mininet> s1 ps -a
```

![20](https://user-images.githubusercontent.com/122883189/231039168-b1b2c14d-973a-465e-897e-679b7cff5115.PNG)

## Uji konektivitas antar host

Sekarang, verifikasi bahwa Anda dapat melakukan ping dari host 0 ke host 1:

```
mininet> h1 ping -c 1 h2
```

![21](https://user-images.githubusercontent.com/122883189/231039524-d21b25e1-96bd-4ac6-ac8c-e7db9843dfb5.PNG)

Cara yang lebih mudah untuk menjalankan tes ini adalah dengan menggunakan perintah pingall bawaan Mininet CLI, yang melakukan ping semua pasangan:

```
mininet> pingall
```

![23](https://user-images.githubusercontent.com/122883189/231040131-0e771b60-2d8a-4725-b1b5-17383c86263c.PNG)

Keluar dari CLI:

```
mininet> exit
```

![24](https://user-images.githubusercontent.com/122883189/231040558-dc78b34d-da79-44b4-9e9c-03710ca30dd3.PNG)

## Pembersihan

Jika Mininet mogok karena alasan tertentu, bersihkan:

```
$ sudo mn -c
```

![25](https://user-images.githubusercontent.com/122883189/231040799-be7b63f3-4ecc-4b66-989c-ff04861ef531.PNG)