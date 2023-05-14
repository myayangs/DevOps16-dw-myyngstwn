# Kelompok 1
Anggota :
- M. Yayang Setiawan
- Muhamad Nafis

# Docker
**Docker** adalah perangkat lunak yang dapat digunakan untuk membuat, menguji, dan menerapkan aplikasi dengan cepat. Docker menjadikan perangkat lunak ke dalam unit yang disebut container, dimana di dalamnya memiliki semua yang diperlukan perangkat lunak agar dapat berfungsi termasuk aplikasi dan dependencies.

## Requirements

- Buat 3 VM dengan spesifikasi sebagai berikut :

|      VM      |  CPU  |  RAM  | Storage |
|    :---:     | :---: | :---: |  :---:  | 
|  Appserver   |   2   | 2 GB  |  20 GB  |
|   Gateway    |   1   | 1 GB  |  20 GB  |
|    CI/CD     |   2   | 2 GB  |  20 GB  |

![image](Media/VM/1.png)

![image](Media/VM/2.png)

## Setup Docker 
Untuk Petunjuk instalasi Docker bisa dilihat pada [Docker](https://docs.docker.com/engine/install/ubuntu/) dan [Digital Ocean](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04).

- Pertama, install Docker di dalam server yang telah dibuat. Bisa gunakan perintah dibawah ini.

```
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
```
![image](Media/Setup%20Docker/1.png)

```
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```
![image](Media/Setup%20Docker/2.png)

```
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

![image](Media/Setup%20Docker/3.png)

```
sudo apt-get update
```

![image](Media/Setup%20Docker/4.png)

```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
![image](Media/Setup%20Docker/5.png)

```
docker -v
```

![image](Media/Setup%20Docker/5.png)

- Kemudian setup untuk root command docker yang akan dipakai nantinya agar saat menggunakan command docker tersebut sudah tidak perlu menggunakan perintah sudo. Bisa gunakan perintah dibawah ini.

```
sudo usermod -aG docker (user)
```
> keterangan : perintah di atas ini adalah suatu perintah untuk mengizinkan user yang digunakan agar dapat menjalankan perintah docker tanpa menggunakan perintah sudo.

![image](Media/Setup%20Docker/7.png)

## Deploy Aplikasi on Top Docker
### Frontend

- git clone repository `Wayshub Frontend`.

```
git clone https://github.com/dumbwaysdev/wayshub-frontend
```

![image](Media/Frontend/1.png)

- Kemudian Intregasikan Frontend dan Backend. Lalu membuat `Dockerfile`. 

![image](Media/Frontend/2.png)

![image](Media/Frontend/3.png)

![image](Media/Frontend/4.png)

### Database

- Membuat docker mysql dan menjalankan dengan docker compose.

![image](Media/Database/1.png)

![image](Media/Database/2.png)

- Kemudian membuat user database.

![image](Media/Database/3.png)

### Backend

- - git clone repository `Wayshub Backend`.

```
git clone https://github.com/dumbwaysdev/wayshub-backend
```

![image](Media/Backend/1.png)

- - Kemudian Intregasikan Backend dan Database. Lalu membuat `Dockerfile`.

![image](Media/Backend/2.png)

![image](Media/Backend/3.png)

### Docker Compose
- Membuat Docker compose dan menjalankannya.
![image](Media/Docker%20Compose/1.png)

![image](Media/Docker%20Compose/2.png)

### Docker Push Images 
- Kemudian melakukan login ke dalam `docker.hub` di dalam terminal.
```
docker login
```
![image](Media/Docker%20Push%20Images/1.png)

- Kemudian memberikan tag dan push pada Image
```
docker tag kel1-frontend myyngstwn/wayshub-frontend
```

```
docker push myyngstwn/wayshub-frontend
```

![image](Media/Docker%20Push%20Images/2.png)

![image](Media/Docker%20Push%20Images/3.png)

## Konfigurasi Reverse Proxy

- Kemudian membuat reverse proxy dan serta certbot sertifikasi pada aplikasi wayshub-frontend dan wayshub-backend.

![image](Media/RP/1.png)

![image](Media/RP/2.png)

![image](Media/RP/3.png)

![image](Media/RP/4.png)

![image](Media/RP/5.png)