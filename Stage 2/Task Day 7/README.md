# Ansible

## Setup Ansible

- Install **Ansible**. Lalu cek Ansible sudah terinstall. Bisa gunakan perintah dibawah ini.

```
sudo apt-add-repository ppa:ansible/ansible
```

```
sudo apt install ansible
``` 

```
ansible --version
```

![image](Media/1.png)

![image](Media/2.png)

- Kemudian setup konfigurasi dengan membuat file:

![image](Media/3.png)

  - `inventory` yang isinya dengan IP dari server yang akan di koneksikan dengan Ansible. 

```
[angka] # name server
123.456.789    # Public IP Address

[all:vars]
ansible_user="" # your username
ansible_pythone_interpreter=/usr/bin/python3
```

![image](Media/4.png)

  - `ansible.cfg`  yang isinya dengan konfigurasi dasar Ansible.

```
[defaults]

# target to the inventory file
inventory = Inventory

# used for ansible to access the server with ssh-key
private_key_file = /home/ubuntu/.ssh/id_rsa

# skipping known_hosts checking
host_key_checking = False

# python intrepreter
interpreter_python = auto_silent
```
![image](Media/5.png)

## Create user

- Pertama buat file `add-user.yaml`. Dan isikan konfigurasi seperti dibawah ini.
```
---
- become: true
  gather_facts: false
  hosts: all
  tasks:
    - name: "Creating User"
      ansible.builtin.user:
        groups: sudo
        name: "{{username}}"
        password: "{{password}}"
        state: present
        append: yes
        home: /home/({username})
  vars:
    - username: # Fill in your desired username
    - password:  # whois encrypted password
```

![image](Media/7.png)

- Untuk password user harus mengisinya dengan password yang sudah di enkripsi, untuk membuat password yang di enkripsi memerlukan package yang bernama `whois`. Install **whois** dan ketikkan password yang akan di enkripsi. Bisa gunakan perintah dibawah ini.

```
sudo apt install whois
```

```
mkpasswd --method=sha-256
```

![image](Media/6.png)

- Setelah mendapatkan password yang sudah di enkripsi, copy password tersebut dan tambahkan kedalam file `add-user.yaml`. Setelah itu jalankan file dengan menggunakan ansible playbook. Bisa gunakan perintah dibawah ini.

```
ansible-playbook add-user.yml
```

![image](Media/8.png)


## Setup Docker dan Menjalakan Aplikasi Wayshub Frontend di Appserver

- Pertama buat file `setup-docker.yaml`. Lalu isikan konfigurasi seperti dibawah ini. Dan jalankan file dengan menggunakan ansible playbook. 

![image](Media/9.png)

![image](Media/10.png)

- Kemudian buat file `docker-wayshub.yml`. Lalu isikan konfigurasi seperti dibawah ini. Dan jalankan file dengan menggunakan ansible playbook.

![image](Media/11.png)

![image](Media/12.png)

- Wayshub frontend telah berhasil di akses di browser 

![image](Media/13.png)

## Setup Nginx

- Pertama konfigurasi domain 

![image](Media/14.png)

- Kemudian buat direktori dan file reverse proxy yang nantinya akan dicopy.
  - rp-app.conf
```
server {
    server_name yyg.studentdumbways.my.id;

    location / {
             proxy_pass http://103.187.146.32:3000;
    }
}
```
  - rp-node-app.conf
```
server { 
    server_name node-app.yyg.studentdumbways.my.id; 
    
    location / { 
             proxy_pass http://103.187.146.32:9100;
    } 
} 
```
  - rp-node-gateway.conf
```
server { 
    server_name node-gateway.yyg.studentdumbways.my.id; 
    
    location / { 
             proxy_pass http://103.13.206.110:9100;
    } 
} 
```
  - rp-prometheus.conf
```
server { 
    server_name prom.yyg.studentdumbways.my.id; 
    
    location / { 
             proxy_pass http://103.250.11.187:9090;
    }
}
```
  - rp-grafana.conf
```
server { 
    server_name dashboard.yyg.studentdumbways.my.id; 
    
    location / {
             proxy_set_header Host dashboard.yyg.studentdumbways.my.id; 
             proxy_pass http://103.250.11.187:3000;
    }
}
```
![image](Media/15.png)

- Kemudian buat file `setup-nginx.yml`. Lalu isikan konfigurasi seperti dibawah ini. Dan jalankan file dengan menggunakan ansible playbook.
![image](Media/16.png)

![image](Media/17.png)

![image](Media/18.png)