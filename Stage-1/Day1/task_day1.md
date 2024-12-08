1. Devops kepanjangan dari Development dan Operasi yang tugasnya coding suatu program, pengelolaan infrastruktur, administrasi sistem, dan keamanan sistem. biasanya devops membuat dan memonitoring suatu vm di staging,production,dan cloud disuatu perushaan.

2. cara membuat multipass pada ubuntu
   
step1: buka terminal di ubuntu

step2: install multipass dengan menggunakan command "sudo snap install multipass"
![alt text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-1/Day1/image/0.png?raw=true)

step3: membuat vm baru / multipass baru dengan nama "day1" menggunakan command "multipass launch --name day1"
![alt text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-1/Day1/image/1.png?raw=true)

step4: check apakah multipass yang baru dibuat tadi sudah berjalan/running dengan menggunakan command "multipass list"
![alt text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-1/Day1/image/2.png?raw=true)

step5: setelah mengecheck status multipass yang sudah berjalan saatnya masuk ke dalam multipass "day1" dengan mengguakan command "multipass shell day1"
![alt text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-1/Day1/image/3.png?raw=true)

3. cara install apache2 pada multipass yang sudah dibuat "day1"
   
step1: masuk kedalam multipass yang sudah dibuat "day1" menggunakan command "multipass shell day1"
![alt text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-1/Day1/image/3.png?raw=true)

step2: intall apache2 dengan menggunakan command "sudo apt install apache2"
![alt text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-1/Day1/image/4.png?raw=true)

step3: setelah apache2 telah terinstall mari check status apache dengan menggunakan command "sudo systemctl status apache2" 
![alt text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-1/Day1/image/5.png?raw=true)


4. cara install nginx
step1: install nginx dengan menggunakan command "sudo apt install nginx"
![alt text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-1/Day1/image/nginx-install.png?raw=true) 

step2: setelah menginstall nginx, check apakah nginx berjalan/terjadi error dengan menggunakan command "systemctl status nginx"
![alt text](https://github.com/tanuwijaya0811/devops22-dumbways-Tanu/blob/main/Stage-1/Day1/image/nginx-status.png?raw=true)
