# Prometheus & Grafana

## Setup Node Exporter

- Install node exporter dengan docker `port 9100` pada **appserver** dan **gateway**. Pertama buat file `node-exporter.yaml`. Lalu isikan konfigurasi seperti dibawah ini. Dan jalankan file dengan menggunakan ansible playbook.

![image](Media/Node%20exporter/1.png)

![image](Media/Node%20exporter/2.png)

![image](Media/Node%20exporter/3.png)

## Setup Prometheus & Grafana

- Pertama buat file `prometheus.yml` yang berfungsi sebagai konfigurasi file prometheus. Lalu install prometheus dengan docker `port 9090` dan grafana dengan docker `port 3000` pada server monitoring. Kemudian melakukan verifikasi apakah node exporter sudah menjadi target prometheus. Dan Selanjutnya mengakses dashboard grafana.
![image](Media/Prometheus/1.png)

![image](Media/2.png)

![image](Media/3.png)

![image](Media/Prometheus/4.png)

![image](Media/Prometheus/5.png)

![image](Media/Grafana/1.png)

### Memmbuat Dashboard
![image](Media/Grafana/2.png)

![image](Media/Grafana/3.png)

![image](Media/Grafana/4.png)

![image](Media/Grafana/5.png)

![image](Media/Grafana/6.png)

![image](Media/Grafana/7.png)

![image](Media/Grafana/8.png)

![image](Media/Grafana/9.png)

![image](Media/Grafana/10.png)

### Membuat Alert
![image](Media/Grafana/11.png)

![image](Media/Grafana/12.png)

![image](Media/Grafana/13.png)

![image](Media/Grafana/14.png)

![image](Media/Grafana/15.png)

![image](Media/Grafana/16.png)
