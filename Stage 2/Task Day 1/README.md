# Cloud Computing

## Setup Front-End

- Buka [Console IDCloudHost](https://console.idcloudhost.com/) dan Login.

![1](https://user-images.githubusercontent.com/54151202/230743232-87ad9b2f-21c1-4518-aea9-dc3e1d032576.png)
![2](https://user-images.githubusercontent.com/54151202/230743235-b121ed3a-7b17-4adb-806f-fc26f61de24c.png)

- Lalu Buat 2 VM dengan spesifikasi sebagai berikut :

|      VM      |  CPU  |  RAM  | Storage |
|    :---:     | :---: | :---: |  :---:  |
|  Appserver   |   1   | 2 GB  |  20 GB  |
|  Gateway     |   1   | 1 GB  |  20 GB  |

![2](https://user-images.githubusercontent.com/54151202/230743240-a26291f3-9671-4849-91d5-2f2ce2316d0e.png)
![3](https://user-images.githubusercontent.com/54151202/230795830-a11c20b3-c228-4df6-a3bf-e6a9c33e4597.png)

- Buka terminal dan akses server `Appserver` menggunakan SSH.

![4](https://user-images.githubusercontent.com/54151202/230743726-a5646b30-bb6f-49a1-a3d7-d28e69cb3e41.png)

- Kemudian Install **NodeJS** dan **NVM** . bisa gunakan perintah dibawah ini.

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
```
```
nvm install 14
```

![5](https://user-images.githubusercontent.com/54151202/230743754-657b2cb8-09b8-4abf-a101-4c65e9499a86.png)

- Kemudian buat  direktori `wayshub ` dan clone repository `Wayshub Frontend`. Lalu masuk ke direktori `wayshub-frontend` dan `npm install`. 

```
git clone https://github.com/dumbwaysdev/wayshub-frontend
```

![6](https://user-images.githubusercontent.com/54151202/230745494-b5f60a0c-bf96-4c4d-8916-ae7f7ad34ab5.png)

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

![7](https://user-images.githubusercontent.com/54151202/230745532-504ab752-3b25-4b74-a611-c0b6e5d1f400.png)
![8](https://user-images.githubusercontent.com/54151202/230745534-8cc39ce8-adc9-49ce-a915-4e5dc3e1daa4.png)

## Setup Domain (Front End) menggunakan Cloudflare

- Buka [Cloudflare](https://dash.cloudflare.com/) dan Login. Lalu pilih domain yang ada diberanda.

![9](https://user-images.githubusercontent.com/54151202/230745561-00cd5d87-5fc9-43dc-959b-0671108e03cb.png)
![10](https://user-images.githubusercontent.com/54151202/230745564-6d496afe-57b9-4fb6-bd74-f7bedf2777c5.png)

- Pilih bagian `DNS` lalu `add record` dan isi nama domain serta public ip dari `IDCloudHost` dan klik save.

![11](https://user-images.githubusercontent.com/54151202/230745566-d8488dd0-0e4c-4c15-a474-327833fe1837.png)

## Konfigurasi Reverse Proxy

- Buka terminal dan akses server `gateway` menggunakan SSH.

![12](https://user-images.githubusercontent.com/54151202/230745595-728dbb32-e6fd-494b-ba92-5cb92d972da4.png)

- Kemudian Install **NGINX**. 

![13](https://user-images.githubusercontent.com/54151202/230745602-af0fd408-15ce-44d0-85f6-eee858900757.png)

- Kemudian masuk ke folder **nginx** setelah itu buat directory baru. Masuk ke direktori yang sudah dibuat tadi, lalu buat file dengan nama `rp-fe.conf`. Dengan masukan konfigurasi berikut:

```
server {
        server_name (domain).my.id;
location / {
         proxy_pass http://(private-ip):3000;
	}
}
```
![14](https://user-images.githubusercontent.com/54151202/230745626-fe94b417-d3ce-4f3c-9b34-3bddcca1fcb2.png)
![15](https://user-images.githubusercontent.com/54151202/230745628-f3e3501f-a251-49a3-a099-f70970db0e65.png)

- Setelah itu simpan file nya, keluar dari direktori `dumbways` dan masuk ke file `nginx.conf` dan tambahkan lokasi direktori yang berisi konfigurasi reverse proxy yang sudah dibuat.

![16](https://user-images.githubusercontent.com/54151202/230745644-100b1a90-b947-4267-91c9-36aa722ef4f6.png)

- Kemudian cek konfigurasi yang sudah dibuat dan reload **NGINX**.

![17](https://user-images.githubusercontent.com/54151202/230745667-ccf27c2b-8e5c-4e5c-92f4-1e4507fc06fb.png)

- Kemudian buka terminal server `appserver` dan masuk ke dalam direktory `wayshub-frontend` lalu jalankan command  `pm2 start ecosystem.config.js` untuk menjalankan aplikasi.

![18](https://user-images.githubusercontent.com/54151202/230745677-0cc98d0c-ee67-48d4-8b2c-8b3b37aff43f.png)

- Kemudian buka browser dan akses domain `yyg.studentdumbways.my.id`.

![19](https://user-images.githubusercontent.com/54151202/230745681-e5753f11-cdd7-40ed-82c3-60662e650142.png)


