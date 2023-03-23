# Web Server and Load Balancing

## Reverse Proxy
**Reverse proxy** adalah konfigurasi standar yang digunakan untuk mengubah jalur traffic, misalkan aplikasi menggunakan port 3000 tetapi agar dapat di akses melalui port 80 maka harus menggunakan reverse proxy. Disini menggunakan webs server nginx yang akan dikonfigurasi dengan reverse proxy.

- Pertama-tama masuk ke folder nginx setelah itu buat directory baru.

```
cd /etc/nginx
```

```
sudo mkdir dumbways
```

- Masuk ke direktori yang sudah dibuat tadi, lalu buat file dengan nama reverse-proxy.conf

```
cd dumbways
```
```
sudo nano reverse-proxy.conf
```

- Kemudian masukkan konfigurasi berikut:
```
server { 
    server_name dumbflix.xyz; 
  
    location / { 
             proxy_pass http://192.168.18.120:3000;
    }
}
```
>pastikan port 3000 di ganti sesuai aplikasi yang digunakan.

- Setelah itu simpan file nya, keluar dari direktori `dumbways` dan masuk ke file `nginx.conf`.

- Kemudian Pergi ke bagian include, lalu masukkan lokasi direktori yang berisi konfigurasi tadi dan simpan.

```
include /etc/nginx/dumbways/*;
```
>`/*;` menandakan file `nginx.conf` akan membaca seluruh file yang berada di dalam directory **dumbways**

- Kemudian cek konfigurasi yang sudah dibuat tadi menggunakan perintah berikut.
```
sudo nginx -t
```

-  Kemudian tinggal melakukan restart/reload Nginx nya.
```
sudo systemctl restart nginx
```
```
sudo systemctl reload nginx
```


- Kemudian buat virtual host, untuk membuat virtual host masuk ke server lokal dan domain ketikkan perintah berikut.

```
sudo nano /etc/hosts
```

```
C:\Windows\System32\drivers\etc\hosts
```

- Kemudian masukkan IP dari server dan nama domain yang di inginkan.

```
192.168.18.120 dumbflix.xyz
```
- Kemudian buka web browser dan ketikkan nama domain tadi, jika keluar 502 bad gateway seperti gambar dibawah, itu sudah benar karena pada server belum di install aplikasi, sekarang coba untuk  aplikasi `dumbflix`.

- Masuk kedalam direktori `dumbflix-frontend` lalu jalankan menggunakan `pm2` setelah itu restart/reload Nginx nya dan Kemudian buka web browser dan ketikkan nama domain tadi.

