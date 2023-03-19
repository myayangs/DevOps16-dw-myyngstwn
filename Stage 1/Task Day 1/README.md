# Introduction to DevOps

## Definisi DevOps
DevOps adalah serangkaian praktik yang mengotomasisasi proses antara pengembangan aplikasi dan tim pengembang agar mereka dapat melakukan proses **_build_**, **_test_** dan **_release_** perangkat lunak lebih cepat dan lebih handal.

## Lifecycle DevOps
- **_Continuous Integration_** : Tim pengembang berkolaborasi satu sama lain untuk mengembangkan  aplikasi.  **_Continuous Integration_** memudahkan pengelolaan kode antar **_developer_**. **_Continuous Integration_** bertujuan untuk otomatisasi, transparansi, dan kolaborasi antara **_developer_** terkait kode yang diproduksi.
- **_Continuous Delivery_** : Dalam **_Continuous Delivery_**, ini terdiri dari fase pengujian dan rilis. **_Continuous Delivery_** dapat membantu memastikan aplikasi siap untuk di **_deploy_** dengan secara otomatis melewati tahap pengujian dan rilis.  
- **_Continuous Deployment_** : Dalam **_Continuous Deployment_** memastikan bahwa publish aplikasi dapat dilakukan tanpa mempengaruhi kinerja dari aplikasi tersebut. Sangat penting untuk memastikan bahwa kode telah diterapkan pada semua server pada fase ini. Proses ini menghilangkan kebutuhan untuk merilis aplikasi secara manual.

## Konsep HyperVisor
Hypervisor adalah sebuah teknik virtualisasi yang memungkinkan beberapa sistem operasi untuk berjalan bersamaan pada sebuah host.

## Operating System
Operating System adalah penghubung antara software dan hardware agar dapat digunakan oleh pengguna.

## Install Ubuntu Server
Sebelum melakukan instalasi ubuntu server, hal pertama yang harus dilakukan adalah menginstall tools virtual machine serta mendownload file ISO ubuntu server terlebih dahulu. Kali ini, akan menggunakan tools VMware Workstation Player sebagai virtual machine. Download [VMware Workstation Player](https://www.vmware.com/asean/products/workstation-player/workstation-player-evaluation.html) dan [ISO Ubuntu Server 20.04](https://ubuntu.com/download/server) 
    

- Setelah melakukan instalasi VMware, buka VmWare. Kemudian klik `“Create a New Virtual Machine”`, Kemudian masukan file ISO Ubuntu yang akan diinstall. Disini pilih saja di bagian `Installer disc image file (iso):`. Dan klik di bagian `Browse` lalu cari lokasi file ISO ubuntu server yang sudah di download sebelumnya lalu klik `Next`.

![image](Media/1.png) 
![image](Media/2.png) 


- Kemudian masukan user dan password yang diinginkan. lalu `Next`.

![image](Media/3.png) 

- Kemudian isi kan nama file program instalasinya. lalu `Next`.

![image](Media/4.png) 

- Kemudian atur size Disk yang akan digunakan instalasi Ubuntu Server disini menggunakan `20 GB` bisa diisi dengan sesuai kebutuhan dan `pilih split virtual disk into multiple files`. lalu `Next`.

![image](Media/5.png) 

- Kemudian Melakukan custom pada hardware. Klik tombol `customize hardware`. Silakan ubah pada bagian Memory ubah menjadi 2GB, lalu processor ubah nilainya menjadi 2-Core CPU dan Network Adapternya pilih Bridged. Disini bisa menyesuaikan dengan kebutuhan. Lalu `Finish`. 

![image](Media/6.png) 

- Menunggu proses persiapan instalasi. Kemudian memilih Bahasa dan Layout Keyboard.

![image](Media/7.png) 
![image](Media/9.png) 

- Kemudian ubah konfigurasi networknya menjadi Manual dan IP Address disesuaikan dengan local network yang terhubung dengan internet.

![image](Media/10.png) 
![image](Media/11.png) 

-Kemudian proxy setting dan Ubuntu Mirror bisa langsung `Done`.

![image](Media/12.png) 
![image](Media/13.png) 

- Kemudian pilih `Custom storage layout` dan sesuaikan dengan kebutuhan. lalu `Done` dan `Continue`.

![image](Media/14.png) 
![image](Media/15.png)
![image](Media/16.png)
![image](Media/17.png)
![image](Media/18.png)

-Kemudian profile config diisi dengan keinginan lalu ceklis pada bagian `Install OpenSSH Server` dan setting fitur.

![image](Media/19.png)
![image](Media/20.png)
![image](Media/21.png)

- Kemudian setelah proses instalasi selesai `Reboot`.

![image](Media/22.png)

- Kemudian Login dengan username dan password yang telah dibuat. lalu memastikan ubuntu sudah terkoneksi pada internet bisa masukan command `ping 8.8.8.8` lalu untuk mengakhiri silahkan tekan ctrl+c.

![image](Media/23.png)

- Kemudian mencoba remote SSH menggunakan windows Terminal.

![image](Media/24.png)
