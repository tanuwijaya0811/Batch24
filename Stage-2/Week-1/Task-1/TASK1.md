# **Panduan Instalasi dan Penggunaan**

Selamat datang di dokumentasi proyek ini! Di bawah ini adalah panduan instalasi dan penggunaan proyek ini. Anda akan menemukan langkah-langkah yang mudah diikuti dan perintah yang dapat disalin langsung.

---

## **1. Server**

Langkah pertama adalah create new user disetiap server dan server dapat login dengan SSH-KEY and password 

### **Create New User**

Create new user dan memberikan akses sudo kepada user baru
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/3.png)

dengan menggunakan command dibawah ini:
```bash
sudo adduser amanda
sudo usermod -aG sudo amanda
```
merubah akses PasswordAuthentication menjadi yes yang ada difolder /etc/ssh/sshd_config.d/ 60-cloudimg-settings.conf agar user baru bisa login dengan password 
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/4.png)

dengan menggunakan command dibawah ini:
```bash
cd /etc/ssh/sshd_config.d/
sudo nano 60-cloudimg-settings.conf
```

masuk kedalam file sshd.config dan uncommand dibagian PubkeyAuthentication dan PasswordAuthentication
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/5.png)

dengan menggunakan command dibawah ini:
```bash
cd /etc/ssh/
sudo nano sshd_config
```

jika sudah melakukan perubahan di ssh langkah berikutnya adalah merestart ssh dengan cara systemctl restart ssh
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/6.png)

dengan menggunakan command dibawah ini:
```bash
sudo systemctl restart ssh
sudo systemctl status ssh
```
jika sudah semua mari kita coba login menggunakan user baru kedalam server 
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/7.png)

---
## **2. Database**
Langkah kedua adalah Deploy database MySQL 

---
menginstall mysql server pada Apps-Server 
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/8.png)

dengan menggunakan command dibawah ini: 
```bash
sudo apt install mysql-server
```
membuat password pada root
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/9.png)
dengan menggunakan command dibawah ini:
```bash
sudo mysql -u root
ALTER USER 'root'@'%' IDENTIFIED BY 'password';
ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'password';
```

jika sudah keluar dari mysql dengan 'ctrl + d' dan setting mysql_secure_installation 
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/10.png)

dengan menggunakan command dibawah ini:
```bash
sudo mysql_secure_installation 
```
setelah mensetting mysql secure installation coba login ke mysql dengan menggunakan password
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/11.png)

dengan menggunakan command dibawah ini:
```bash
sudo mysql -u root -p
```

setalah itu buat database baru dan membuat table baru di mysql
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/12.png)

dengan menggunakan command dibawah ini:
```bash
#melihat semua database yang ada
show databases;

#create new database
CREATE demo;

#cara menggunakan database yang ada
USE demo;

#menampilkan semua table yang ada;
show tables;

#membuat table baru
CREATE TABLE transaction(
id serial PRIMARY KEY,
nama_barang VARCHAR (30) UNIQUE NOT NULL
harga_barang VARCHAR (100) NOT NULL
);
```
memasukkan sebuah data kedalam table di mysql
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/13.png)

dengan menggunakan command dibawah ini:
```bash
INSERT INTO transaction(nama_barang, harga_barang)
VALUES
('sepatu', 'Rp.500.000'),
('sendal', 'Rp.100.000'),
('baju', 'Rp.500.000'),
('celana', 'Rp.200.000');

#meliat semua isi sebuah table
select * from transaction;
```

Cara mengupdate sebuah table dan menghapus sebuah table di mysql
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/14.png)

dengan menggunakan command dibawah ini:
```bash
#UPDATE DATA
UPDATE transaction
SET harga_barang = 'Rp.60.000'
WHERE nama_barang = 'baju';

#meliahat perubahan
select * from transaction

#MENGHAPUS SEBUAH DATA
DELETE FROM transaction
WHERE nama_barang = 'celana';


#meliahat perubahan 
select * from transaction
```

Membuat user baru dan memberikan privileges pada mysql database
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/15.png)

dengan menggunakan command dibawah ini:
```bash
#Create user Admin
CREATE USER 'admin'@'%' IDENTIFIED BY 'password';

#memberikan semua akses database yang ada di mysql
GRANT ALL PRIVILEGES ON *.* TO 'admin'@'%';

#restart privileges
FLUSH PRIVILEGES;
```

Coba masuk ke user admin 
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/16.png)

dengan menggunakan command dibawah ini:
```bash
#masuk menggunakan user admin
sudo mysql -u admin -p

#check database yang ada
show databases;
```

membuat user baru untuk guest yang hanya bisa mengakses database demo 
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/17.png)

dengan menggunakan command dibawah ini:
```bash
#Create user Guest
CREATE USER 'guest'@'%' IDENTIFIED BY 'password';

#memberikan semua akses database yang ada di mysql
GRANT ALL PRIVILEGES ON demo.* TO 'guest'@'%';

#restart privileges
FLUSH PRIVILEGES;
```

Coba menggunakan user guest 
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/18.png)

dengan menggunakan command dibawah ini:
```bash
#masuk kedalam mysql dengan mengunakan user guest
sudo mysql -u guest -p

#melihat semua databases
show databases;

```

---
## **3. Backend**
Langkah ke tiga adalah mensetting backend di Gatewayserver

---

pada gambar disebelah kiri cara menginstall web server nginx dan yang sebelah kanan membuat database dumbflix pada Apps-Server; 
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/19.png)

dengan menggunakan command dibawah ini:
```bash
#diserver Gateway menginstall nginx gambar sebelah kiri
sudo apt install nginx -y

#########
#diserver Apps-server membuat database gambar sebelah kanan
CREATE DATABASE dumbflix;

#melihat semua database;
show databases;
```
merubah settingan bind-address dan mysqlx-bind-address yang ada di pada mysql/mysql.conf.d 
![Alt Text]([https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/24.png](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/24.png))

dengan menggunakan command dibawah ini:
```bash
#masuk ke dalam folder /etc/mysql/mysql.conf.d
cd /etc/mysql/mysql.conf.d

#melihat isi folder
ls

#mengedit file mysqld.cnf
sudo nano mysqld.cnf

```
---

Cloning github backend pada GatewayServer digambar sebelah kiri dan Cloning github frontend pada Apps-Server digambar sebelah kanan
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/20.png)

dengan menggunakan command dibawah ini:
```bash
#git  clone backend
git clone https://github.com/dumbwaysdev/dumbflix-backend.git

#git  clone frontend
git clone https://github.com/dumbwaysdev/dumbflix-frontend.git

```

langkah berikutnya adalah menginstall nvm di GatewayServer 
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/21.png)

dengan menggunakan command dibawah ini:
```bash
#menginstall nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash

#lakukan exec
exec bash

#install node 14
nvm i 14

#check version node
node -v

```

masuk kedalam folder dumbflix-backend yang ada diGatewayServer lalu baca terlebih dahulu README.md dan lakukan perintah yang ada di README.md
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/22.png)

dengan menggunakan command dibawah ini:
```bash
#masuk kedalam folder
cd dumbflix-backend

#meliat list folder dan file
ls

#melihat isi file README.md
cat README.md

#melihat isi file .env.example
cat .env.example

#mengcopy file .env.example
cp .env.example .env

#melihat isi file .env
cat .env

```

merubah config/config.json ke database yang ada di Apps-Server, gambar disebelah kiri adalah gambar diGatewayServer dan gambar disebelah kiri adalah IP dari Apps-Server yang akan di masukkan kedalam GatewayServer
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/23.png)

dengan menggunakan command dibawah ini:
```bash
  "development": {
      #username yang digunakan untuk login ke mysql
    "username": "admin",
      #password yang digunakan untuk login ke mysql
    "password": "password",
      #database yang ada di mysql
    "database": "dumbflix",
    #ip server Apps-Server
    "host": "103.127.139.127",
    "dialect": "mysql",
    "operatorsAliases": false
  },
  "test": {
    "username": "root",
    "password": null,
    "database": "database_test",
    "host": "127.0.0.1",
    "dialect": "mysql",
    "operatorsAliases": false
  },
  "production": {
    "username": "root",
    "password": null,
    "database": "database_production",
    "host": "127.0.0.1",
    "dialect": "mysql",
    "operatorsAliases": false
  }
}

```

Setelah itu install sequlize didalam server GatewayServer
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/25.png)

dengan menggunakan command dibawah ini:
```bash
#install sequlize
npm i sequlize-cli -g

```

Setelah menginstall sequelize, lakukan migrasi database backend ke frontend. seperti gambar di bawah ini (sebelah kiri GatewayServer dan sebelah kanan Apps-Server)
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/26.png)

dengan menggunakan command dibawah ini:
```bash
#migrasi database
npx sequlize db:migrate


#diserver Apps-Server
#masuk ke mysql untuk mengecheck nya
sudo mysql -u admin -p

#melihat semua isi dabases;
show databases;

#gunakan database dumbflix
USE dumbflix;

#melihat semua isi table yang ada di dumbflix;
show tables;
```

install pm2 pada Gateway-Server
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/27.png)

dengan menggunakan command dibawah ini:
```bash
#install pm2
npm i pm2 -g

#membuat script dengan pm2
pm2 init simple 
```

edit file pm2 yang sudah di buat ( ecosystem.config.js )
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/28.png)

dengan menggunakan command dibawah ini:
```bash
# meliaht list file dan folder
ls

#melihat isi file ecosystem.config.js
cat ecosystem.config.js

#mengedit file ecosystem.config.js
nano ecosystem.config.js


#isi script rubah bagian nama menjadi dumbflix-backend dan script menjadi npm start
# module.exports = {
#  apps : [{
#    name   : "dumbflix-backend",
#    script : "npm start"
#  }]
#}

#menjalankan program backend dengan pm2
pm2 start ecosystem.config.js

```

membuat folder dan file didalam /etc/nginx dan mensetting nginx.conf
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/29.png)
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/30.png)
dengan menggunakan command dibawah ini:
```bash
#masuk ke folder /etc/nginx
cd /etc/nginx

#membuat folder apps
sudo mkdir apps

#menambahkan perintah didalam file nginx.conf 
# menambahkan include /etc/nginx/apps/*; pada nginx.conf
sudo nano nginx.conf




#melihat isi file nginx.conf
cat nginx.conf

```

menambahkan file didalam /etc/nginx/apps di GatewayServer
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/31.png)

dengan menggunakan command dibawah ini:
```bash
#masuk kedalam folder /etc/nginx/apps
cd /etc/nginx/apps

#membuat file api.tanu.studentdumbways.my.id
sudo nano api.tanu.studentdumbways.my.id

#isi file api.tanu.studentdumbways.my.id
#server{
#      server_name api.tanu.studentdumbways.my.id;
#
#      location / {
#                proxy_pass http://localhost:5000;
#      }
#}




melihat isi file api.tanu.studentdumbways.my.id
cat api.tanu.studentdumbways.my.id


```

install certbot di galam GatewayServer
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/32.png)

dengan menggunakan command dibawah ini:
```bash
#install certbot
sudo snap install --classic certbot

#certbot command
sudo ln -s /snap/bin/certbot /usr/bin/certbot

```

membuat folder .secrets dan membuat file di dalam .secrets
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/33.png)

dengan menggunakan command dibawah ini:
```bash
#membuat folder .secrets
sudo mkdir .secrets

#masuk ke folder .secrets
cd .secrets

#membuat file demo.ini
sudo nano demo.ini

#isi file demo.ini
#dns_cloudflare_email = "email cloudflare"
#dns_cloudflare_api_key = "Global API Key cloudflare"

```


change mode file demo.ini dan menjalan kan certbot 
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/35.png)

dengan menggunakan command dibawah ini:
```bash
#masuk ke dalam folder .secrets
cd .secrets

#gunakan ll untuk menunjukkan rincian list
ll

#change mode menjadi read
chmod 400 demo.ini

#kembali ke home
cd

#check status nginx -t 
sudo nginx -t 

#jalankan certbot
sudo certbot

```

open browser lalu coba jalankan api.tanu.studentdumbways.my.id apakah sudah berjalan / belum 

![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/36.png)


---
## **4. Frontend**
Langkah ke empat adalah mensetting dan menjalankan apikasi frontend di Apps-Server

---

change url backend di dalam file /src/config/api.js
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/37.png)

dengan menggunakan command dibawah ini:
```bash
#baca README.md untuk melihat apa saja yang perlu di lakukan
cat README.md

#masuk ke folder /src/config/
cd src/config

#melihat list config
ls

#melihat isi file api.js
cat api.js

#edit api.js
#rubah url baseURL: menjadi 'https://api.tanu.studentdumbways.my.id/api/v1'
nano api.js

```

jika sudah selesai kembali ke folder dumbflix-frontend lalu install npm dan pm2
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/38.png)

dengan menggunakan command dibawah ini:
```bash
#masuk ke folder dumbflix-frontend
cd dumbflix-frontend

#install npm
npm i

#install pm2
npm i pm2 -g

```

buat script untuk menjalankan frontend yang ada di Apps-Server dengan menggunakan pm2
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/39.png)
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/40.png)
dengan menggunakan command dibawah ini:
```bash
#untuk membuat script ecosystem.config.js seperti di backend
pm2 init simple

#melihat isi ecosystem.config.js
cat ecosystem.config.js

#rubah dibagian name dan script
nano ecosystem.config.js

#jalankan frontend dengan pm2 
pm2 start ecosystem.config.js
```


mencoba menjalankan frontend di browser dengan ip address Apps-Server dan port 3000
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/41.png)

menambahkan reverse proxy di GatewayServer danbagian sebelah kanan adalah penambahan subdomain
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/42.png)
dengan menggunakan command dibawah ini:
```bash
#masuk kedalam folder /etc/nginx/apps
cd /etc/nginx/apps

#buat file untuk reverse proxy
sudo nano tanu.studentdumbways.my.id
#tambahkan script dibawah ini untuk menyambungkan frontend
#server {
#	server_name tanu.studentdumbways.my.id;
#
#	location / {
#		proxy_pass http://103.127.139.127:3000; #ip yg digunakan adalah ip server frontend
#	}
#}

#setelah sudah check apakah ada script yang error dengan nginx -t
sudo nginx -t

#reload dan restart nginx service
sudo systemctl reload nginx
sudo systemctl restart nginx

```
Jika sudah selesai buka tab browser baru lalu coba masukkan subdomain yang sudah dibuat tanu.studentdumbways.my.id
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/43.png)

Setelah itu tambahkan sertificate certbot agar domain tanu.studentdumbways.my.id menjadi secure
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/44.png)
dengan menggunakan command dibawah ini:
```bash
sudo certbot

#setelah menambahkan sertificate certbot masuk kembali ke /etc/nginx/apps/
cd /etc/nginx/apps

#check list folder dan file 
ls

#lihat isi script tanu.studentdumbways.my.id
cat tanu.studentdumbways.my.id
#didalamnya terlihat sudah ada tambahan ssl_sertificate
```

Jika sudah selesai buka tab browser baru lalu coba masukkan  tanu.studentdumbways.my.id dan lihat apakah sudah secure
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/45.png)

marikita coba register. disini saya sudah register dan dapat login
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/46.png)

Mari kita check apakah didatabase Users bertambah. disini kita gunakan Apps-Server dan masuk kedalam mysql
![Alt Text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-2/Week-1/Task-1/images/47.png)

dengan menggunakan command dibawah ini:
```bash
#masuk kedalam mysql 
sudo mysql -u admin -p 

#melihat semua database yang ada
show databases;

#menggunakan database dumbflix
USE dumbflix;

#menampilkan semua table yang ada di dumbflix
show tables;

#melihat semua isi table Users
select * from Users

```
