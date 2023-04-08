# Cloud Computing

## Setup Front-End

- Buka [Console IDCloudHost](https://console.idcloudhost.com/) dan Login.

- Lalu Buat 2 VM dengan spesifikasi sebagai berikut :

|      VM      |  CPU  |  RAM  | Storage |
|    :---:     | :---: | :---: |  :---:  |
|  Appserver   |   1   | 2 GB  |  20 GB  |
|  Gateway     |   1   | 1 GB  |  20 GB  |

- Buka terminal dan akses server `Appserver` menggunakan SSH.

- Kemudian Install **NodeJS** dan **NVM** . bisa gunakan perintah dibawah ini.

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
```
```
nvm install 14
```

- Kemudian buat direktori `wayshub ` dan clone repository `Wayshub Frontend`. Lalu masuk ke directory `wayshub-frontend` dan `install npm`. 

```
git clone https://github.com/dumbwaysdev/wayshub-frontend
```

- Kemudian Install **PM2**. Lalu buat dan edit konfigurasi `ecosystem pm2`.
```
npm install pm2 -g 
```
```
pm2 init simple
```
```
sudo nano ecosystem.config.js
```

## Setup Domain (Front End) menggunakan Cloudflare

- Buka [Cloudflare](https://dash.cloudflare.com/) dan Login. Lalu pilih domain yang ada diberanda.

- Pilih bagian `DNS` lalu `add record` dan isi nama domain serta public ip dari `IDCloudHost` dan klik save.

## Konfigurasi Reverse Proxy

- Buka terminal dan akses server `gateway` menggunakan SSH.

- Kemudian Install **NGINX**. 
- Kemudian masuk ke folder **nginx** setelah itu buat directory baru. Masuk ke direktori yang sudah dibuat tadi, lalu buat file dengan nama `rp-fe.conf`. Dengan masukan konfigurasi berikut:

```
server {
        server_name (domain).my.id;
location / {
         proxy_pass http://(private-ip):3000;
	}
}
```  

- Setelah itu simpan file nya, keluar dari direktori `dumbways` dan masuk ke file `nginx.conf` dan tambahkan lokasi direktori yang berisi konfigurasi reverse proxy yang sudah dibuat.

- Kemudian cek konfigurasi yang sudah dibuat dan reload **nginx**.

- Kemudian buka terminal server `appserver` dan masuk ke dalam direktory `wayshub-frontend` lalu jalankan command  `pm2 start ecosystem.config.js` untuk menjalankan aplikasi.

- Kemudian buka browser dan akses domain `yyg.studentdumbways.my.id`
