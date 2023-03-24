# Web Server and Load Balancing

## Reverse Proxy
**Reverse proxy** adalah konfigurasi standar yang digunakan untuk mengubah jalur traffic, misalkan aplikasi menggunakan port 3000 tetapi agar dapat di akses melalui port 80 maka harus menggunakan reverse proxy. Disini menggunakan webs server nginx yang akan dikonfigurasi dengan reverse proxy.

- Pertama-tama masuk ke folder nginx setelah itu buat directory baru.

```
cd /etc/nginx
```

![1](https://user-images.githubusercontent.com/54151202/227259661-47965515-2380-4ebb-b7ed-4a649bdbc8f2.png)

```
sudo mkdir dumbways
```

![2](https://user-images.githubusercontent.com/54151202/227259732-51ec020a-93f5-47e6-850e-27246cd870ba.png)


- Masuk ke direktori yang sudah dibuat tadi, lalu buat file dengan nama reverse-proxy.conf

```
cd dumbways
```
```
sudo nano reverse-proxy.conf
```
![3](https://user-images.githubusercontent.com/54151202/227259839-d50b2741-9e96-4d08-b713-2c14731180a8.png)

- Kemudian masukkan konfigurasi berikut:
```
server { 
    server_name dumbflix.xyz; 
  
    location / { 
             proxy_pass http://192.168.18.120:3000;
    }
}
```
![4](https://user-images.githubusercontent.com/54151202/227259934-37cf1444-b611-41e5-a494-69731c0b4b90.png)
>pastikan port 3000 di ganti sesuai aplikasi yang digunakan.

- Setelah itu simpan file nya, keluar dari direktori `dumbways` dan masuk ke file `nginx.conf`.

```
sudo nano nginx.conf
```

![5](https://user-images.githubusercontent.com/54151202/227260064-ab91215e-5335-4014-b1a5-8ea08096d63e.png)

- Kemudian Pergi ke bagian `include`, lalu masukkan lokasi direktori yang berisi konfigurasi tadi dan simpan.

```
include /etc/nginx/dumbways/*;
```

![6](https://user-images.githubusercontent.com/54151202/227260396-4455f0f3-0001-4bcf-9983-120c55aac51d.png)
>`/*;` menandakan file `nginx.conf` akan membaca seluruh file yang berada di dalam directory **dumbways**

- Kemudian cek konfigurasi yang sudah dibuat tadi menggunakan perintah berikut.
```
sudo nginx -t
```
![7](https://user-images.githubusercontent.com/54151202/227260499-87f6f03b-50fe-42cb-902e-18941d320c95.png)

-  Kemudian tinggal melakukan restart/reload Nginx nya.
```
sudo systemctl restart nginx
```
```
sudo systemctl reload nginx
```
![8](https://user-images.githubusercontent.com/54151202/227261815-5509a2cc-0cc4-4e74-b840-67f57a9ad7ed.png)

- Kemudian buat virtual host, untuk membuat virtual host masuk ke server lokal dan domain ketikkan perintah berikut.

```
sudo nano /etc/hosts
```
![9](https://user-images.githubusercontent.com/54151202/227258469-86dc8249-a0cc-42ef-9642-ecf8bb9c95ac.png)

```
C:\Windows\System32\drivers\etc\hosts
```
![10](https://user-images.githubusercontent.com/54151202/227259440-900481af-705c-4cfb-8014-5acae4607e59.png)

- Kemudian masukkan IP dari server dan nama domain yang di inginkan.

```
192.168.18.120 dumbflix.xyz
```
![11](https://user-images.githubusercontent.com/54151202/227258361-cb900bfa-7de8-4be8-98f0-013d3b88ffdd.png)

![12](https://user-images.githubusercontent.com/54151202/227258382-a36e2614-68e1-45f8-bee5-14f4188280c5.png)


- Kemudian buka web browser dan ketikkan nama domain tadi, jika keluar 502 bad gateway seperti gambar dibawah, itu sudah benar karena pada server belum di install aplikasi, sekarang coba untuk  aplikasi `dumbflix`.

![13](https://user-images.githubusercontent.com/54151202/227257748-ae6e8044-226e-4eb8-93c6-126db191f787.png)

- Masuk kedalam direktori `dumbflix-frontend` lalu jalankan menggunakan `pm2` setelah itu restart/reload Nginx nya dan Kemudian buka web browser dan ketikkan nama domain tadi.

![14](https://user-images.githubusercontent.com/54151202/227257573-a41d9871-e708-4cc8-b351-674723935e2f.png)

![15](https://user-images.githubusercontent.com/54151202/227257613-58a78bdb-b9a0-411a-a6b0-f25f869f68b9.png)


# Challenge
## Load Balancing
`Load Balancing` adalah suatu jaringan komputer yang menggunakan metode untuk mendistribusikan beban kerjaan pada dua atau bahkan lebih suatu koneksi jaringan secara seimbang agar pekerjaan dapat berjalan optimal dan tidak overload (kelebihan) beban pada salah satu jalur koneksi.

- Untuk membuat konfigurasi `load balancing`, buatlah satu server baru terlebih dahulu dan install aplikasi pada server baru tersebut.

![16](https://user-images.githubusercontent.com/54151202/227425281-7f9ca2e9-e99c-47e2-804c-4f1d496dd606.png)

![17](https://user-images.githubusercontent.com/54151202/227425275-298d33a0-09ce-4818-b94f-16ada3e029a9.png)

![18](https://user-images.githubusercontent.com/54151202/227425279-5c0c2a14-227e-416b-8bb1-290bf0c6414c.png)

- Sekarang sudah punya 2 server untuk aplikasinya, lalu membuat konfigurasi `load balancing`, masuk ke file konfigurasi `reverse proxy` yang sudah dibuat tadi dan tambahkan konfigurasi dibawah ini.

```
sudo nano reverse-proxy.conf
```

![19](https://user-images.githubusercontent.com/54151202/227425248-5f2d8098-1f0b-4470-b619-487cae175ac6.png)

- Kemudian tambahkan konfigurasi ke dalam file `reverse-proxy.conf`. dapat menggunakan konfigurasi di bawah ini.
```
upstream domain { 
    server 192.168.18.120:3000;
    server 192.168.18.200:3000;
}
server { 
    server_name dumbflix.xyz; 
  
    location / { 
             proxy_pass http://domain;
    }
}
```

![20](https://user-images.githubusercontent.com/54151202/227425338-10ae8413-7a66-4227-a412-039fbf6f0b91.png)

> Pada bagian upstream dapat mengganti nama domain dengan nama yang diinginkan. Pada bagian server masukan IP dari server, setelah itu diikuti dengan port aplikasi. Selanjutnya pada bagian proxy_pass ubah dari yang sebelumnya adalah alamat IP dari aplikasi, sekarang samakan dengan nama upstream yang ada di konfigurasi. Jika sudah sekarang cek apakah konfigurasi yang sudah dibuat tadi itu error atau tidak.
```
sudo nginx -t 
```

![21](https://user-images.githubusercontent.com/54151202/227425349-99339420-f0a4-43a8-8e5d-d1e267af8ac5.png)

- Kemudian restart/reload nginx untuk memperbarui konfigurasi yang sudah dibuat.
```
sudo systemctl reload nginx
```
![22](https://user-images.githubusercontent.com/54151202/227425375-e4b61aeb-729a-4bb7-a758-b38ef762cbee.png)

- Kemudian jalankan aplikasi yang ada pada server ini, dan cek di browser menggunakan domain tadi.

![23](https://user-images.githubusercontent.com/54151202/227425454-9401ba4c-bf68-464b-baaa-24c668b2433e.png)
![15](https://user-images.githubusercontent.com/54151202/227257613-58a78bdb-b9a0-411a-a6b0-f25f869f68b9.png)

- Kemudian untuk mengecek apakah `load balancing` sudah berjalan atau tidak, coba matikan satu server dan refresh webnya.

![24](https://user-images.githubusercontent.com/54151202/227425466-7ee57305-3440-4438-aa97-b5b6784fc880.png)
![15](https://user-images.githubusercontent.com/54151202/227257613-58a78bdb-b9a0-411a-a6b0-f25f869f68b9.png)
