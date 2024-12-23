Reference :
[PM2 reference](https://pm2.keymetrics.io/)

Task
1. Jelaskan menurutmu apa perbandingan antara Application Monolith & Application Microservices
   Jawaban:
   - Monolith adalah pengembangan aplikasi dimana seluruh komponennya digabungkan dalam satu aplikasi besar.

    - Microservices adalah aplikasi yang dibangun sebagai serangkaian layanan kecil yang indempenden dan terpisah, mempunyai fungsi yang spesifik. 
   
2. Deploy Simple application NodeJS, Golang & Python dengan menampilkan nama masing-masing
    Jawaban:
   - NodeJs
      1. donwload nodejs dengan command curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
      2. lakukan exec bash
      3. setelah itu install npm dengan command sudo apt install npm
      4. buat script index.js
      5. setelah itu npm install express --save
      6. jika belum bisa check status ufw, lalu beri akses ke port 3000,22,3100

   -Python
     1. install python dengan command sudo apt install python-pip -y
     2. lalu install flask dengan command pip install flask
     3. buat script index.py
     4. jalankan script dengan perintah python3 index.py
  
    -GO
     1. install go dengan command wget https://go.dev/dl/go1.23.4.linux-amd64.tar.gz
     2. hapus installasi sebelumnya rm -rf /usr/local/go && tar -C /usr/local -xzf go1.23.4.linux-amd64.tar.gz
     3. tambahkan user export PATH=$PATH:/usr/local/go/bin
     4. buat script main.go
     5. jalankan script dengan go run main.go
   

   
4. Deploy aplikasi berikut [dumbflix](https://github.com/dumbwaysdev/dumbflix-frontend), dengan menggunakan `node version 14`
    Jawaban:
   -

5. Implementasikan penggunaan PM2 agar aplikasi kalian dapat berjalan di background (simple-app-node, simple-app-python, dumbflix)
    Jawaban:
   - NodeJs
     1. install pm2 dengan command npm install -g pm2
     2. jalankan pm2 dengan command pm2 start index.js
    
   - Python
     1. jalankan pm2 dengan command pm2 start index.py
    
   - Go
     1. jalankan pm2 dengan command pm2 start main.go
