# Manage Server with Terminal

## Teks Manipulation
Berikut adalah beberapa perintah yang dapat digunakan dalam *Teks Manipulation*

### A. **cat**
`cat` adalah perintah yang digunakan membuat satu atau beberapa file, melihat isi file, serta menggabungkan dua buah file menjadi satu file.

```
cat > (file-name)
```
> untuk membuat suatu file baru serta memasukkan teks, Jika sudah menambakan teks dapat keluar dengan klik `CTRL + D`.

```
cat (file-name)
```
> untuk melihat isi dari suatu file

```
cat day5 day6 > final
```
> untuk menggabungkan dua buah file, dan menyimpannya ke dalam `final`

### B. **sed**
`sed` adalah singkatan dari stream editor. Gunanya untuk memanipulasi teks dasar pada file. Dengan sed dapat mengganti teks dengan cepat.

```
sed -i 's/with/dengan/g' final
```
>mengganti semua kata `with` menjadi `dengan` pada `final`

3. **grep**
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
> kan mencari semua file yang berisikan kata `Server`

4. **sort**
`Sort` untuk mengurutkan data, baik itu secara ascending atau descending.

```
sort number
```
>untuk mengurutkan berdasarkan ascending

```
sort -r number
```
>untuk mengurutkan berdasarkan descending

5. **echo**
`echo` digunakan untuk mencetak string / pesan dari hasil perintah lain.

```
echo "Hello Dumbways!"
```
>untuk mencetak string **

```
echo "Hello Dumbways!" >> final
```
>untuk mencetak kata Hello Dumbways! di `final`    

```
echo "BootCamp DevOps" > day1
```
>untuk mereplace semua data di `final` dan menggantinya dengan `BootCamp DevOps`


## Network Firewall Bash

Untuk melakukan Instalasi ufw menggunakan perintah dibawah ini.
```
sudo apt install ufw -y
```

Untuk mengaktifkan firewall menggunakan perintah dibawah ini.
```
sudo ufw enable
```
untuk melihat status firewall menggunakan perintah dibawah ini.
```
sudo ufw status
```
Untuk Memberikan akses ufw kepada port 22, 80, 443 dan 3000 Update apt dan install nginx menggunakan script bash. Pertama uatlah file terlebih dahulu yang akan berfungsi sebagai tempat kosong untuk script bash yang akan diketik.
```
nano ufw.sh
```





## Monitoring

### A. **htop**
`htop` merupakan perintah untuk memonitoring sistem, dan dapat melihat penggunaan memory, cpu, swap. Berikut adalah contoh penggunaannya, apabila belum terinstall maka install dulu menggunakan perintah dibawah.

```
sudo apt install htop -y
```
```
htop
```

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

Untuk menjalankan `nmon` kalian dapat menggunakan perintah dibawah ini.
```
nmon
```
Keterangan : Disini dapat memilih ingin memonitoring apa saja, Disini coba untuk menampilkan beberapa saja.

- c adalah CPU
- m adalah Memory
- d adalah Disk
- n adalah network


## Bash Script

