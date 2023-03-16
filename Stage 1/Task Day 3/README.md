# Application in Server

## Node JS

- Pertama-tama lakukan instalasi **_Node.js_** versi 10. bisa gunakan perintah dibawah ini.

```
nvm install 10
```
![1](https://user-images.githubusercontent.com/54151202/225574904-5e6762f8-2c4d-46a4-bb57-080f699d8da3.png)

- Clone Repository `dumbflix-frontend`
```
git clone https://github.com/dumbwaysdev/dumbflix-frontend.git
```
![2](https://user-images.githubusercontent.com/54151202/225574925-ca233b41-00e9-4b71-b68c-9443182c11c6.png)

- Kemudian masuk ke directory `dumbflix-frontend` dan install npm yang sudah ada di project dengan cara:
```
npm install
```
![3](https://user-images.githubusercontent.com/54151202/225574940-58430a06-aae9-4260-bc67-694ca90a48ca.png)

- Kemudian konfigurasi `api.js`

![4](https://user-images.githubusercontent.com/54151202/225644297-73cad95a-4287-434d-bcc8-5aaef6e31197.png)
![5](https://user-images.githubusercontent.com/54151202/225574974-90a10d33-ffd9-4b19-aa92-d46659e31982.png)


- Kemudian untuk menjalankan aplikasi dapat menggunakan perintah
```
npm start
```
-Kemudian akses web browser dengan `IP` dan port `:3000`.

![6](https://user-images.githubusercontent.com/54151202/225574981-956498a9-2a4d-4a20-ba6f-23acae3571d9.png)


## Golang

- Pertama-tama install terlebih dahulu engine-nya. Untuk instalasi kalian bisa menggunakan beberapa perintah dibawah ini.
```
wget https://golang.org/dl/go1.16.5.linux-amd64.tar.gz && sudo su
```
![1](https://user-images.githubusercontent.com/54151202/225761925-7fbf91e7-7925-4553-b327-2b5b7b6d7393.png)


```
rm -rf /usr/local/go && tar -C /usr/local -xzf go1.16.5.linux-amd64.tar.gz && exit
```
![2](https://user-images.githubusercontent.com/54151202/225761929-1b046509-21e7-4dfa-9360-c7dbb7298498.png)

- Selanjutnya masukkan path **_go_** pada `.bashrc`
```
sudo nano .bashrc
```
![3](https://user-images.githubusercontent.com/54151202/225761905-7a962eec-596d-4226-82f7-b6af1c4de2bd.png)

```
export PATH=$PATH:/usr/local/go/bin
```
![4](https://user-images.githubusercontent.com/54151202/225761909-0dbb6e4d-f540-4c90-b9be-96f1fedd2c16.png)

- Jika sudah, lakukan verifikasi apakah **_go_** sudah terinstall dengan perintah berikut:
```
go version
```
![5](https://user-images.githubusercontent.com/54151202/225761912-7a870b8d-8434-4434-b862-2aaa7369a791.png)

Buat sebuah file dengan nama `app.go`.
```
nano index.go
```

- Setelah itu masukkan script dibawah ini.
```
package main

import "fmt"

func main() {
    fmt.Println("Halo, saya <isi nama kalian>!")
}
```
![6](https://user-images.githubusercontent.com/54151202/225761913-88b2130e-5910-4644-9533-fe25158684fa.png)

- Sekarang jalankan aplikasi **_go_** dengan menggunakan perintah berikut.
```
go run index.go
```
![7](https://user-images.githubusercontent.com/54151202/225761915-c1d94abf-ba80-47c3-8a70-75d0cbdfad35.png)

- Jika aplikasi ingin di build, maka jalankan perintah berikut ini.
```
go build index.go
```
![8](https://user-images.githubusercontent.com/54151202/225761919-53cd46f2-3fe1-41f7-996c-a6e56a309e38.png)

- Jika sudah jalankan aplikasi dengan menggunakan perintah berikut.
```
./app
```
![9](https://user-images.githubusercontent.com/54151202/225761922-29b41791-b4d4-472f-944c-fe9e24d567fe.png)


## Python
![1](https://user-images.githubusercontent.com/54151202/225761838-ea83cb3e-7e75-41b9-a346-72484995e411.png)

![2](https://user-images.githubusercontent.com/54151202/225761843-fe55c715-70d1-42fa-a68c-59dd793f7c45.png)

![3](https://user-images.githubusercontent.com/54151202/225761845-b341888f-6a1a-4c55-8622-4ca180a1f14f.png)

![4](https://user-images.githubusercontent.com/54151202/225761847-fcc08b12-d429-461e-95d8-096a92327669.png)

![5](https://user-images.githubusercontent.com/54151202/225761849-360cdf6c-dd55-449b-a007-48afb51402b6.png)

![6](https://user-images.githubusercontent.com/54151202/225761854-da02a36b-a3f7-4801-8f35-f08e4a01ed9b.png)
