### load balancing system
Load Balancing adalah proses mendistribusikan lalu lintas jaringan (network traffic) atau beban kerja ke beberapa server secara efisien. Bayangkan seperti seorang polisi lalu lintas yang mengatur kendaraan di persimpangan agar tidak menumpuk di satu jalur saja, melainkan dibagi rata ke semua jalur yang tersedia.

pada task ini, Load Balancing didefinisikan sebagai teknik yang diperlukan untuk mencapai high-availability (ketersediaan tinggi) dari suatu aplikasi dengan cara melakukan proses scaling (memperbanyak) aplikasi menjadi lebih dari satu instance dan mengkonfigurasi proxy load balancer untuk membagi tugas di antara mereka.

load balancing memiliki beberapa fungsi diantaranya
* Mencapai High-Availability (Ketersediaan Tinggi): Memastikan aplikasi tetap dapat diakses meskipun salah satu server mengalami gangguan. Jika satu server mati, beban akan dialihkan ke server lain yang masih hidup.
* Fault Tolerance (Toleransi Kesalahan): Sistem menjadi lebih tahan banting terhadap kegagalan komponen. Modul ini secara spesifik menyebutkan bahwa materi ini adalah bagian dari pembahasan tentang Fault Tolerance dalam Sistem Terdistribusi.
* Scaling (Skalabilitas): Memungkinkan aplikasi untuk diperbesar kapasitasnya dengan mudah (menjadi lebih dari satu instance) untuk menangani beban yang lebih besar.

untuk implementasi konsep load balancing pada task ini menggunakan komponen-komponen berikut:
* Load Balancer (Nginx): Modul menggunakan Nginx sebagai perangkat lunak proxy yang bertugas membagi beban. Nginx dikonfigurasi dalam file nginx.conf menggunakan blok upstream backend yang mendefinisikan grup server aplikasi yang akan menerima trafik.
* Backend Application (Blacksheep): Aplikasi yang menanggung beban kerja adalah aplikasi web berbasis Python yang dibuat menggunakan framework Blacksheep. Aplikasi ini bertindak sebagai "pekerja" yang memproses permintaan dari user.
* Orkestrasi & Scaling (Docker Compose): Implementasi teknisnya menggunakan Docker Compose. Dalam file docker-compose.yml, didefinisikan layanan bs_app (aplikasi) dan nginx . Kunci dari implementasinya ada pada perintah eksekusi yang menggunakan fitur scaling: --scale bs_app=2. Perintah ini secara otomatis membuat 2 kontainer aplikasi Blacksheep yang identik.

#### gambaran singkat mekanisme load balancing dalam task ini
1. Pengguna mengakses localhost pada port 80 yang dijaga oleh Nginx.
2. Nginx meneruskan permintaan tersebut (proxy_pass) ke grup upstream backend.
3. Karena ada 2 instance aplikasi (bs_app-1 dan bs_app-2) yang berjalan, Nginx akan membagi permintaan tersebut ke kedua aplikasi tersebut.
4. Hal ini dibuktikan melalui log (docker logs), di mana terlihat permintaan masuk ditangani secara bergantian atau terdistribusi ke instance yang berbeda.
