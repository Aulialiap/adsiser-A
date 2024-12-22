#  Multi Web Server Application Deployment

## Pendahuluan
Proyek ini bertujuan untuk mengimplementasikan deployment aplikasi web multi-server dengan menggunakan teknologi modern, seperti Docker dan AWS CLI. Infrastruktur yang dibangun mencakup database SQL, caching menggunakan Redis, load balancing dengan HAProxy, dan dua web server berbasis Nginx.

### Latar Belakang
Dengan meningkatnya kebutuhan terhadap aplikasi berbasis web, diperlukan infrastruktur server yang handal, efisien, dan mampu menangani skala yang lebih besar. Proyek ini memberikan pengalaman praktis dalam pengelolaan infrastruktur server dengan teknologi modern, termasuk kontainerisasi menggunakan Docker.

### Lingkup Pekerjaan
Cakupan pekerjaan yang dilakukan meliputi:
- Pembuatan infrastruktur dengan 3 instance server untuk MySQL, Redis, HAProxy, dan dua web server berbasis Nginx.
- Teknologi yang digunakan: AWS CLI, Docker Container.
- Pengujian akses server melalui HTTP dan SSH.
- Dokumentasi kendala untuk evaluasi.

## Perancangan Sistem
### Arsitektur Sistem
Arsitektur sistem terdiri dari:
- Database Server : MySQL dalam container untuk menyimpan data aplikasi.
- Caching Server : Redis dalam container untuk mempercepat akses data.
- Load Balancer : HAProxy dalam container untuk mendistribusikan traffic ke web server lain.
- Web Servers : Dua container berbasis Nginx dengan menerapkan Website Wordpress yang merupakan website open source.
- Infrastruktur diimplementasikan dengan Docker dan Docker Compose.
- Terdiri dari 3 instance:
  1. Instance Webserver 1 using Docker Container: Wordpress, MySQL, Nginx, Redis (Alpine Ver.) 
  2. Instance Webserver 2 using Docker Container: Wordpress, MySQL, Nginx, Redis (Alpine Ver.) 
  3. Instance Load Balancer: Happroxy


### Teknologi yang Digunakan
- **AWS CLI**: Manajemen sumber daya cloud.
- **Docker dan Docker Compose**: Kontainerisasi aplikasi dan orkestrasi layanan.
- **Redis**: Caching server.
- **HAProxy**: Load balancer.
- **Nginx**: Web server.
- **MySQL**: Database untuk aplikasi.

## Implementasi
### Langkah-Langkah Implementasi
1. **Instance Webserver 1**:
   - Instalasi paket: `apt-transport-https`, `ca-certificates`, `curl`, dan lainnya.
   - Unduh dan instal Docker, aktifkan layanan Docker.
   - Buat direktori konfigurasi WordPress (`wordpress-nginx`).
   - Konfigurasi file `docker-compose.yml` (yang berisi service wordpress, redis, mysql, nginx) dan `nginx.conf`.
   - Jalankan layanan dengan `docker-compose up -d`.

2. **Instance Webserver 2**:
   - Langkah-langkah konfigurasi sama dengan Webserver 1.

3. **Instance Load Balancer (HAProxy):**
   - Instalasi HAProxy dengan `apt install haproxy`.
   - Konfigurasi file `/etc/haproxy/haproxy.cfg` untuk mengatur frontend dan backend.
   - Uji validitas konfigurasi dengan `haproxy -c -f /etc/haproxy/haproxy.cfg`.
   - Mulai ulang layanan HAProxy.

4. **Redis Cache:**
   - Instalasi Redis Tools.
   - Konfigurasi WordPress untuk integrasi Redis di file `wp-config.php`.

5. **Pengaturan Keamanan:**
   - Konfigurasi firewall untuk mengizinkan akses HTTP dan SSH.
   - Pengaturan Elastic IP untuk mengakses layanan secara publik.

### Studi Kasus
**Tujuan:** Membuat aplikasi web multi-server yang terintegrasi dengan Redis, MySQL, dan HAProxy dan dua web server berbasis Nginx.

**Langkah:**
- Manual setting instance di AWS EC2.
- Instalasi Docker dan Docker Compose.
- Deployment layanan Redis, MySQL, dan Nginx dalam container menggunakan Docker Compose.

**Hasil yang diharapkan :**
Aplikasi web dapat diakses melalui load balancer dengan caching dari Redis dan data tersimpan di MySQL.

## Pengujian dan Hasil
### Pengujian
- Mengakses aplikasi web melalui load balancer.
- Verifikasi caching Redis melalui log.
- Pengujian koneksi ke database MySQL.

### Hasil
- Aplikasi web berhasil diakses melalui load balancer (HAProxy).
- Redis berfungsi sebagai caching server.
- Database MySQL dapat menyimpan dan mengambil data sesuai kebutuhan.

## Analisis dan Evaluasi
### Evaluasi Hasil
Proyek berhasil diimplementasikan sesuai rencana. Penggunaan Docker dan Docker Compose menyederhanakan deployment layanan.

### Kendala dan Solusi
**Kendala:**
- Penyesuaian firewall untuk mengizinkan akses HTTP dan SSH.
- Debugging konfigurasi HAProxy.

**Solusi:**
- Menggunakan log AWS untuk memeriksa konfigurasi security group.
- Mengacu pada dokumentasi resmi HAProxy untuk konfigurasi load balancing.

## Kesimpulan dan Rekomendasi
### Kesimpulan
Proyek berhasil mencapai tujuannya. Infrastruktur multi-server memungkinkan aplikasi web berjalan secara efisien dan dapat diskalakan.

### Rekomendasi
- Tambahkan monitoring untuk memastikan ketersediaan layanan.
- Terapkan sistem backup otomatis untuk meningkatkan keamanan data.

## Lampiran
- File konfigurasi Docker Compose dan HAProxy.
- Log hasil eksekusi.
- Tangkapan layar pengujian.
