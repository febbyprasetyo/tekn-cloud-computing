# Diagram - Docker Compose

## Diagram

![Diagram drawio](https://github.com/febbyprasetyo/tekn-cloud-computing/assets/122883189/7f3a4c54-7dd4-46ef-9553-500af715d1ae)

## Penjelasan keterkaitan antara komponen-komponen tersebut:

- Docker image adalah template yang digunakan untuk membuat container. Image berisi sistem operasi, perangkat lunak, dan dependensi yang diperlukan untuk menjalankan aplikasi di dalam container.

- Docker container adalah wadah yang menjalankan instance aplikasi. Container dibuat berdasarkan Docker image dan berjalan dalam lingkungan terisolasi.

- Dockerd (Docker Engine) adalah komponen inti dari Docker yang bertanggung jawab untuk mengelola container. Dockerd berinteraksi dengan kernel sistem operasi untuk membuat dan menjalankan container.

- Docker client adalah antarmuka baris perintah atau API yang digunakan untuk berinteraksi dengan dockerd. Docker client memungkinkan pengguna untuk mengirimkan perintah dan permintaan ke dockerd untuk mengelola container.

- Docker compose adalah alat yang digunakan untuk mendefinisikan dan menjalankan aplikasi multi-container. Dengan menggunakan file konfigurasi YAML, docker compose memungkinkan pengguna untuk mendefinisikan konfigurasi aplikasi yang kompleks dengan beberapa layanan dan dependensi.

- Docker swarm adalah fitur yang memungkinkan pengguna untuk mengelola cluster dari beberapa host Docker. Docker swarm memungkinkan pengguna untuk mengelola dan menyeimbangkan beban aplikasi di seluruh host, serta menyediakan keandalan dan skala otomatisasi.






