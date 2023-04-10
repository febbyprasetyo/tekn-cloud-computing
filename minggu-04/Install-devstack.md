# Penerapan OpenStack di Ubuntu 20.04/18.04 dengan DevStack

## Langkah 1: Perbarui Sistem Ubuntu

Masuk ke sistem Ubuntu Anda - Bisa Desktop atau VM di Cloud dan perbarui.

```
sudo apt update
sudo apt -y upgrade
sudo apt -y dist-upgrade
```

Nyalakan ulang setelah pembaruan

```
sudo reboot
```

## Langkah 2: Tambahkan Stack User

Untuk instalasi Ubuntu 20.04/18.04 lainnya, jalankan perintah di bawah ini untuk membuat pengguna penerapan DevStack.

```
feby@feby-VirtualBox:~$ sudo useradd -s /bin/bash -d /opt/stack -m stack
```

Aktifkan hak istimewa sudo untuk pengguna ini tanpa memerlukan kata sandi.

```
feby@feby-VirtualBox:$ echo "stack ALL=(ALL) NOPASSWD: ALL" | sudo tee /etc/sudoers.d/stack
stack ALL=(ALL) NOPASSWD: ALL
````

Uji koneksi internet Anda dan versi python

```
feby@feby-VirtualBox:$ sudo -u stack
```

![10](https://user-images.githubusercontent.com/122883189/230849879-bc6d73a9-3ea2-4e85-a875-258e4f633b49.PNG)

## Langkah 3: Download DevStack

Repo devstack berisi skrip yang menginstal OpenStack dan templat untuk file konfigurasi.

```
feby@feby-VirtualBox:$ git clone https://opendev.org/openstack-dev/devstack
```

Buat file local.conf dengan 4 password dan alamat Host IP.

```
feby@feby-VirtualBox:~$ cd devstack
feby@feby-VirtualBox:~/devstack$ nano local.conf
```

Menambahkan

```
[[local|localrc]]
ADMIN_PASSWORD=AdminStrongSecret
DATABASE_PASSWORD=$ADMIN_PASSWORD
RABBIT_PASSWORD=$ADMIN_PASSWORD
SERVICE_PASSWORD=$ADMIN_PASSWORD
```

![9](https://user-images.githubusercontent.com/122883189/230850543-69b1c495-dce0-4b08-9b4c-d61d37e43790.PNG)

## Langkah 4: Mulai Penerapan Openstack di Ubuntu 20.04/18.04 dengan DevStack

Sekarang setelah Anda mengonfigurasi konfigurasi minimum yang diperlukan untuk memulai dengan DevStack, mulailah penginstalan Openstack.

```
feby@feby-VirtualBox:~/devstack$ FORCE=yes ./stack.sh
```

DevStack akan menginstal; Ini akan memakan waktu 15 – 20 menit, sebagian besar tergantung pada kecepatan koneksi internet Anda. Di akhir proses instalasi, Anda akan melihat output seperti ini:

```
This is your host IP address: 192.168.10.100
This is your host IPv6 address: 2a01:4f8:c2c:308e::1
Horizon is now available at http://192.168.10.100/dashboard
Keystone is serving at http://192.168.10.100/identity/

The default users are: admin and demo
The password: StrongAdminSecret
```

![8](https://user-images.githubusercontent.com/122883189/230764523-61931d10-177e-4175-81fc-9751a7f2fed6.PNG)