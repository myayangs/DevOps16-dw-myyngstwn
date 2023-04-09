# Manage Database with Backend

## Instalasi dan Konfigurasi Database

- Buka terminal dan akses server `Appserver` menggunakan SSH.

- Kemudian Install **Mysql server**. bisa gunakan perintah dibawah ini.

```
sudo apt install mysql-server
```

![1](https://user-images.githubusercontent.com/54151202/230795917-0aedef43-8a5f-45b9-a70a-95f223b9cb2b.png)

- Kemudian jalankan mysql dan buat password untuk root.

```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```

![2](https://user-images.githubusercontent.com/54151202/230795974-2e7d4a43-949f-47bd-af4a-b226a7ecd770.png)

- Kemudian mengamankan database Mysql. bisa gunakan perintah dibawah ini.

```
sudo mysql_secure_installation
```

![3](https://user-images.githubusercontent.com/54151202/230795999-59f88aeb-515f-4f63-ac59-7545b76c1a97.png)

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

![4](https://user-images.githubusercontent.com/54151202/230796015-05660016-f37b-42bc-8f17-237b6f46432f.png)


- Kemudian masuk kedalam user yang telah dibuat dan membuat database baru. 

```
CREATE DATABASE (db name);
```

![5](https://user-images.githubusercontent.com/54151202/230796022-ca0a3fff-bef6-4d7a-a6c3-319513e3b4d2.png)

## Setup Back-End

- Masuk  direktori `wayshub ` dan clone repository `Wayshub Backend`. Lalu masuk ke direktori `wayshub-backend` dan `npm install`. 

```
git clone https://github.com/dumbwaysdev/wayshub-backend
```
![1](https://user-images.githubusercontent.com/54151202/230796207-b7803b54-1bb3-4f32-8a99-bd2b4e6ee9d0.png)

- Kemudian buat dan edit konfigurasi `ecosystem pm2`.

```
pm2 init simple
```
```
sudo nano ecosystem.config.js
```

![2](https://user-images.githubusercontent.com/54151202/230796217-daf3782d-42df-4f0b-a8ce-f1857f52f839.png)

![3](https://user-images.githubusercontent.com/54151202/230796219-26b50222-764c-4784-9448-253581d9edb9.png)

- Kemudian  instalasi `sequelize cli`.

```
npm install sequelize-cli
```

![4](https://user-images.githubusercontent.com/54151202/230796275-f182664b-92fd-460d-91ed-dc73011cfab6.png)

- Kemudian melakukan konfigurasi di dalam file `config/config.json` untuk melakukan migrasi.
> - user adalah user dari mysql. 
> - password adalah password dari user mysql. 
> - database adalah nama database yang telah dibuat.
> - host adalah alamat dari server database.

![5](https://user-images.githubusercontent.com/54151202/230796292-b4090ecd-da60-46bd-b8e5-18043d2567d3.png)

![6](https://user-images.githubusercontent.com/54151202/230796297-85915dd8-c0d8-4c1a-a2d5-f7ad2544da81.png)

- Kemudian melakukan migrasi data dari backend ke server database yang telah dibuat. bisa gunakan perintah dibawah ini.

```
sequelize db:migrate
```

![7](https://user-images.githubusercontent.com/54151202/230796307-b13cf46f-ebf9-4a3a-8e6e-00a2c178a30e.png)

- Kemudian masuk dalam database untuk memastikan apakah migrasi datanya behasil atau tidak.

![8](https://user-images.githubusercontent.com/54151202/230796314-5caff345-3a89-4f7f-a086-0d1da3c5212e.png)

## Setup Domain (Back-End) menggunakan Cloudflare

- Buka [Cloudflare](https://dash.cloudflare.com/)

- Pilih bagian `DNS` lalu `add record` dan isi nama domain serta public ip dari `IDCloudHost` dan klik save.

![9](https://user-images.githubusercontent.com/54151202/230796371-a2ddd66b-b4ec-4acc-b8ae-348de5714be2.png)

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

![10](https://user-images.githubusercontent.com/54151202/230796457-2b8ae7a6-ce31-40ca-80ee-cbff669df1d8.png)

- Kemudian cek konfigurasi yang sudah dibuat dan reload **NGINX**.

![11](https://user-images.githubusercontent.com/54151202/230796462-22c884af-4965-4023-a9fa-cb7582e969e3.png)

## Intregasi Front-End dan Back-End

- Kemudian buka terminal server `appserver`.

- Masuk ke direktori `wayshub-frontend` dan edit file `src/config/api.js`

![1](https://user-images.githubusercontent.com/54151202/230796473-1c5c996c-6611-40ac-860a-201e25dd7c60.png)

- Kemudian ubah pada bagian baseURL sesuaikan dengan lokasi dari server backend.

![2](https://user-images.githubusercontent.com/54151202/230796483-a441fa3b-7e18-47ea-8959-5203fda65914.png)

- Kemudian buka terminal server `appserver` lalu jalankan aplikasi `wayshub-frontend` dan `wayshub-backend`.

![3](https://user-images.githubusercontent.com/54151202/230796489-7220f537-3f08-4443-9cad-e6e4a90627c1.png)

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

![1](https://user-images.githubusercontent.com/54151202/230796505-7e13dcf5-2f48-4a1e-8705-b3440afac4c5.png)

- Kemudian memastikan perintah `Certbot` dapat dijalankan. Lalu jalankan `Certbot` untuk konfigurasi dan mendapatkan sertifikat.
```
sudo ln -s /snap/bin/certbot /usr/bin/certbot
```
```
sudo certbot --nginx
```

![2](https://user-images.githubusercontent.com/54151202/230796500-35a51b96-a596-47e8-8c3c-126478d91bf7.png)

- Kemudian buka browser akses domain `yyg.studentdumbways.my.id` dan `api.yyg.studentdumbways.my.id`. 
