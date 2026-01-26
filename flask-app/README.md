### Containerized Application
Containerized App (CA) didefinisikan sebagai aplikasi yang dimaksudkan untuk dijalankan oleh container (seperti Docker dan Podman ditask ini). Secara sederhana adalah metode pembungkusan aplikasi di mana kode program disatukan dengan semua dependensi (pustaka/library) dan konfigurasi yang diperlukannya agar dapat berjalan secara konsisten di mana saja.

Tujuan utama pembuatan CA dalam konteks task ini adalah mengubah aplikasi web standar (dalam hal ini tutorial Flask) menjadi format yang portabel dan terisolasi. Dengan mengubahnya menjadi CA, aplikasi tidak lagi bergantung pada konfigurasi sistem operasi host secara langsung, melainkan berjalan di atas environment yang sudah didefinisikan secara ketat di dalam container.

#### Langkah-langkah implementasi pembuatan CA
1. Persiapan Sumber Kode (Source Code): Mengambil kode sumber aplikasi blog dari tutorial Flask (flask/examples/tutorial) dan menyalinnya ke direktori kerja flask-app
2. Persiapan Pembuatan Image (Pembuatan Dockerfile): Implementasi inti ada pada pembuatan file bernama Dockerfile di dalam direktori aplikasi. File ini berisi instruksi membangun lingkungan container:
    * Base Image: Menggunakan python:3.13 sebagai dasar sistem.
    * Direktori Kerja: Membuat dan menetapkan /flask-app sebagai direktori kerja di dalam container.
    * Menyalin File: Memasukkan semua kode dari komputer lokal ke dalam folder /flask-app/ di container.
    * Instalasi Dependensi: Menjalankan perintah pip install -e . untuk menginstal aplikasi dan kebutuhan Python-nya di dalam container.
    * Inisialisasi Database: Menjalankan flask --app flaskr init-db agar database siap digunakan saat container berjalan.
    * Ekspos Port: Membuka port 5000 agar bisa diakses dari luar.
    * Perintah Utama: Menetapkan perintah flask run agar aplikasi otomatis berjalan saat container dinyalakan.
3. Pembangunan Image (Building): Mengubah instruksi Dockerfile tersebut menjadi sebuah image siap pakai dengan nama flaskr:1.0.0 menggunakan perintah:
```
sudo docker build -f Dockerfile -t flaskr:1.0.0 ..
```
4. Menjalankan Container (Running): Menjalankan image tersebut menjadi proses aktif (container). Implementasi di modul ini memetakan port 5001 di komputer Anda ke port 5000 milik container, sehingga aplikasi bisa diakses melalui browser di alamat http://localhost:5001.


karena untuk implementasinya 2 yaitu menggunakan docker dan podman jadi ada sedikit pembeda antara keduanya ketika pembuatan imagenya jika menggunakan yang docker maka perintahnya:
```
sudo docker build -f Dockerfile -t flaskr:1.0.0 ..
```
dan jika menggunakan podman maka perintahnya:
```
podman build -f Dockerfile -t flaskr:1.0.0 ..
```

