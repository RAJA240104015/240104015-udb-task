# 240104015-udb-task
# 📌 UDB Docker Task — MySQL & phpMyAdmin (NIM: 240104015)

Repository ini dibuat untuk memenuhi tugas membuat container **MySQL** dan **phpMyAdmin** menggunakan **Docker Compose**, kemudian dipush ke branch `dev-docker` bersamaan dengan tutorial cara menjalankan project ini.

---

## 📁 Struktur Repository

.
├── docker-compose.yml
└── README.md


---

# 🚀 1. Menyiapkan GitHub + Branch

### 1. Membuat repository
Nama repo:  
240104015-udb-task


### 2. Membuat branch `dev-docker`
Jalankan di WSL:

git checkout -b dev-docker



Push branch pertama kali:

git push -u origin dev-docker
2. Menggunakan SSH untuk GitHub
Untuk melakukan push tanpa username/password, SSH diaktifkan.

1. Generate SSH Key
ssh-keygen -t ed25519 -C "emailgithub@example.com"
2. Aktifkan ssh-agent
eval "$(ssh-agent -s)"
3. Tambahkan SSH key
ssh-add ~/.ssh/id_ed25519
4. Copy public key
cat ~/.ssh/id_ed25519.pub
Tambahkan ke GitHub:
👉 Settings → SSH and GPG Keys → New SSH Key

5. Test koneksi
ssh -T git@github.com

Output sukses:
Hi <username>! You've successfully authenticated.



3. Docker Compose (MySQL + phpMyAdmin)
Isi file docker-compose.yml:

services:
  mysql:
    image: mysql:latest
    container_name: mysql_server
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: mydb
    ports:
      - "3306:3306"
    volumes:
      - mysql_data:/var/lib/mysql

  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    container_name: my_phpmyadmin
    environment:
      PMA_HOST: mysql
    ports:
      - "8080:80"
    depends_on:
      - mysql

volumes:
  mysql_data:


  
4. Cara Menjalankan Project
Jalankan di folder project:
docker compose up -d


Akses:
phpMyAdmin:
http://localhost:8080

MySQL:
host: localhost
user: root
pass: root

Hentikan container:
docker compose down

Reset semua data:
docker compose down -v



5. SOLUSI MASALAH YANG DITEMUI
1. Error SSH: “could not open a connection to your authentication agent”
Solusi:

eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

2. Error SSH: Permission denied (publickey)
Penyebab: SSH key belum ditambahkan ke GitHub.
Solusi:
Tambahkan .pub ke GitHub
Set permission:
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub
chmod 700 ~/.ssh

3. Error saat push: rejected (fetch first)
! [rejected] dev-docker -> dev-docker (fetch first)
Penyebab: branch remote berbeda dengan lokal.
Solusi yang dipakai:
git push origin --delete dev-docker
git push -u origin dev-docker

5. WSL tidak bisa akses folder di drive D:
Gunakan path:
/mnt/d/zKULIAH/Management_jaringan/WSL/udb-docker
