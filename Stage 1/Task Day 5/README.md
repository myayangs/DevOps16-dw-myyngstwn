# Manage Server with Terminal

## Teks Manipulation
Berikut adalah beberapa perintah yang dapat digunakan dalam *Teks Manipulation*

### A. **cat**
`cat` adalah perintah yang digunakan membuat satu atau beberapa file, melihat isi file, serta menggabungkan dua buah file menjadi satu file.

```
cat > day5
```
> untuk membuat suatu file baru serta memasukkan teks, Jika sudah menambakan teks dapat keluar dengan klik `CTRL + D`.

```
cat day5
```
> untuk melihat isi dari suatu file

```
cat day5 day6 > final
```
> untuk menggabungkan dua buah file, dan menyimpannya ke dalam `final`

![cat](https://user-images.githubusercontent.com/54151202/226976730-fd07f4f3-28f5-410c-950b-235b1251cb2e.png)


### B. **sed**
`sed` adalah singkatan dari stream editor. Gunanya untuk memanipulasi teks dasar pada file. Dengan `sed` dapat mengganti teks dengan cepat.

```
sed -i 's/with/dengan/g' final
```
>mengganti semua kata `with` menjadi `dengan` pada `final`

![sed](https://user-images.githubusercontent.com/54151202/226976775-df429dc0-6b5e-486a-8ec8-66d9f7ac2b54.png)


### C. **grep**
`grep` merupakan perintah untuk melakukan pencarian sebuah text dalam sebuah file yang telah dibuat.

```
grep  Server final
```
> akan mencari kata `Server` pada `final`

```
grep  -c Server final
```
> akan menghitung jumlah kata `Server` pada `final`

```
grep  Server *
```
> akan mencari semua file yang berisikan kata `Server`

![grep](https://user-images.githubusercontent.com/54151202/226976863-f354c616-3ea6-4cae-b812-0eeefb8d36ae.png)


### D. **sort**
`sort` untuk mengurutkan data, baik itu secara ascending atau descending.

```
sort TM
```
>untuk mengurutkan berdasarkan ascending

```
sort -r TM
```
>untuk mengurutkan berdasarkan descending

![sort](https://user-images.githubusercontent.com/54151202/226976914-d3fa1a93-165b-44f5-b7b7-a15d2453353c.png)


### E. **echo**
`echo` digunakan untuk mencetak string / pesan dari hasil perintah lain.

```
echo "Welcome Home"
```
>untuk mencetak string **

```
echo "Stage1 Stage2" >> Pre-Bootcamp
```
>untuk mencetak kata `Stage1 Stage2` di `Pre-Bootcamp`    

```
echo "BootCamp DevOps" > Pre-Bootcamp
```
>untuk mereplace semua data di `Pre-Bootcamp` dan menggantinya dengan `BootCamp DevOps`

![echo](https://user-images.githubusercontent.com/54151202/226976964-897afb33-c379-4ba8-8015-5e2f100ea2a4.png)


## Network Firewall Bash

Untuk melakukan Instalasi ufw menggunakan perintah dibawah ini.

```
sudo apt install ufw -y
```

![ufw 1](https://user-images.githubusercontent.com/54151202/226983703-7f0be1af-1af3-4018-b94e-7ceebed4c072.png)


Untuk mengaktifkan firewall menggunakan perintah dibawah ini.

```
sudo ufw enable
```

![ufw 2](https://user-images.githubusercontent.com/54151202/226983753-3a0cf066-55f6-41c6-8986-496460fb6ba0.png)


Untuk Memberikan akses ufw kepada port 22, 80, 443, 3000. Update apt dan install nginx menggunakan script bash. Pertama buatlah file terlebih dahulu yang akan berfungsi sebagai tempat kosong untuk script bash yang akan diketik. Lalu isi script tersebut seperti dibawah ini. 

```
nano firewall-allow
```
```
sudo ufw allow 22
sudo ufw allow 80
sudo ufw allow 443
sudo ufw allow 3000

sudo apt install nginx
sudo apt update
```

lalu jalankan script tersebut dengan perintah dibawah ini.

```
bash firewall-allow
```

![ufw3](https://user-images.githubusercontent.com/54151202/226984558-8eb4ffd5-d1a4-495b-94d4-20f64d46f35f.png)


untuk melihat status firewall menggunakan perintah dibawah ini.

```
sudo ufw status
```

![ufw5](https://user-images.githubusercontent.com/54151202/226985911-09c85be4-1697-4e1c-965f-26ddb1d1a1fe.png)


## Monitoring

### A. **htop**
`htop` merupakan perintah untuk memonitoring sistem, dan dapat melihat penggunaan memory, cpu, swap. Berikut adalah contoh penggunaannya, apabila belum terinstall maka install dulu menggunakan perintah dibawah.

```
sudo apt install htop -y
```

![htop1](https://user-images.githubusercontent.com/54151202/226981638-689e4633-17e8-46b5-af34-a9373f9c7bfa.png)

```
htop
```

![htop2](https://user-images.githubusercontent.com/54151202/226981687-0d71674d-1e23-411a-941b-0361af2a29cf.png)

Keterangan: 
- **CPU** adalah berapa jumlah core yang dimiliki.
- **Mem** adalah total penggunaan memory.
- **Swp** adalah memory cadangan.
- **Tasks** adalah aplikasi yang sedang berjalan di server.
- **Load average** adalah rata-rata aplikasi yang berjalan.
- **Uptime** adalah berapa lama server hidup.
- **PID** adalah nomor proses id setiap proses yang berjalan di linux.
- **VIRT** adalah memory yang terpakai.
- **Command**** adalah perintah apa yang sedang di jalankan.

### A. **nmon**
Untuk instalasi `nmon` dapat menggunakan perintah berikut :
```
sudo apt install nmon
```
![nmon1](https://user-images.githubusercontent.com/54151202/226982071-5c47a15f-5d81-4cff-b632-4b11c3216427.png)



Untuk menjalankan `nmon` kalian dapat menggunakan perintah dibawah ini.
```
nmon
```

![nmon2](https://user-images.githubusercontent.com/54151202/226982017-b9348c45-10d8-42b7-acdc-24c00dbf7cbe.png)

![nmon3](https://user-images.githubusercontent.com/54151202/226982027-f23b0dfd-6592-4e8d-a9f4-af647aac9b77.png)

Keterangan : Disini dapat memilih ingin memonitoring apa saja, Disini coba untuk menampilkan beberapa saja.

- c adalah CPU
- m adalah Memory
- d adalah Disk
- n adalah network

### Challenge
## Bash Script

- Buatlah file terlebih dahulu yang akan berfungsi sebagai tempat kosong untuk script bash yang akan diketik.  Lalu isi script tersebut seperti dibawah ini. 

![bash1](https://user-images.githubusercontent.com/54151202/226996016-037b19fb-22f1-473c-afd2-26a9b37c65b5.png)

![bash2](https://user-images.githubusercontent.com/54151202/226996026-62664f65-0948-4afe-8f7b-b440552425d7.png)

- Untuk menjalankan aplikasi NodeJS(dumbflix-frontend) dengan mengaktifkan firewall menggunakan perintah dibawah ini dan membuka akses port 3000. Lalu jalankan aplikasi tersebut.

![bash3](https://user-images.githubusercontent.com/54151202/226996059-7470ea4f-56b3-4a45-a848-e2ee8ce81bf4.png)

![bash4](https://user-images.githubusercontent.com/54151202/226996063-3d3b5fad-1367-4ca8-8fd4-98ad8284edf3.png)
