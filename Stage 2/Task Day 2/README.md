# Manage Database with Backend

## Instalasi dan Konfigurasi Database

- Buka terminal dan akses server `Appserver` menggunakan SSH.

- Kemudian Install **Mysql server**. bisa gunakan perintah dibawah ini.

```
sudo apt install mysql-server
```

- Kemudian jalankan mysql dan buat password untuk root

- Setelah selesai, tahap selanjutnya adalah mengamankan database. bisa gunakan perintah dibawah ini.

```
sudo mysql_secure_installation
```

- Kemudian masuk sebagai root dan membuat user baru. Lalu beri user privilege.
```
sudo mysql -u root -p
```

```
CREATE USER 'newuser'@'%' IDENTIFIED BY 'password';
```

```
GRANT ALL PRIVILEGES ON *.* TO 'newuser'@'%';
```

```
FLUSH PRIVILEGES;
```

- Kemudian masuk kedalam user yang telah dibuat dan membuat database baru. 

```
CREATE DATABASE (db name);
```

## Setup Back-End

- Masuk  direktori `wayshub ` dan clone repository `Wayshub Backend`. Lalu masuk ke direktori `wayshub-backend` dan `npm install`. 

```
git clone https://github.com/dumbwaysdev/wayshub-backend
```

- Kemudian buat dan edit konfigurasi `ecosystem pm2`.

```
pm2 init simple
```
```
sudo nano ecosystem.config.js
```

- Kemudian  instalasi `sequelize cli`.
```
npm install sequelize-cli
```

- Kemudian melakukan konfigurasi di dalam file `config/config.json` untuk melakukan migrasi.
> - user adalah user dari mysql. 
> - password adalah password dari user mysql. 
> - database adalah nama database yang telah dibuat.
> - host adalah alamat dari server database.

- Kemudian melakukan migrasi data dari backend ke server database yang telah dibuat. bisa gunakan perintah dibawah ini.

```
sequelize db:migrate
```

- Kemudian memeriksa database apakah berhasil atau tidak di migrasi.

## Setup Domain (Back-End) menggunakan Cloudflare

- Buka [Cloudflare](https://dash.cloudflare.com/)


- Pilih bagian `DNS` lalu `add record` dan isi nama domain serta public ip dari `IDCloudHost` dan klik save.

## Intregasi Front-End dan Back-End

- Masuk ke direktori `wayshub-frontend` dan edit file `src/config/api.js`

- Kemudian ubah pada bagian baseURL sesuaikan dengan lokasi dari server backend.

## Konfigurasi Reverse Proxy 

- Buka terminal dan akses server `gateway` menggunakan SSH.

- Kemudian masuk ke folder **nginx/dumbways** lalu buat file dengan nama `rp-be.conf`. Dengan masukan konfigurasi berikut.

```
server {
        server_name (domain).my.id;
location / {
         proxy_pass http://(private-ip):5000;
	}
}
```

- Kemudian cek konfigurasi yang sudah dibuat dan reload **NGINX**.

- Kemudian buka terminal server `appserver` lalu jalankan aplikasi `wayshub-frontend` dan `wayshub-backend`.

# Challenge
## Install SSL on Nginx 
- Agar domain bisa terkoneksi dengan aman perlu menggunakan [Certbot](https://certbot.eff.org/instructions?ws=nginx&os=ubuntufocal).

- Instalasi `Core` dan `Certbot`.
```
sudo apt install snapd
```
```
sudo snap install core; sudo snap refresh core
```
```
sudo snap install --classic certbot
```

- Kemudian memastikan perintah `Certbot` dapat dijalankan. Dan Jalankan `Certbot` untuk konfigurasi dan mendapatkan sertifikat.
```
sudo ln -s /snap/bin/certbot /usr/bin/certbot
```
```
sudo certbot --nginx
```

- Kemudian buka browser akses domain `yyg.studentdumbways.my.id` dan `api.yyg.studentdumbways.my.id`. 
