# Jarkom-Modul-2-E11-2021
## Anggota Kelompok :
| Nama | NRP |
|------|-----|
|Rizqi Rifaldi|05111940000068|
|Yusuf Anfasya|05111940000077|
|Muhammad Subhan|05111940000204|

Pada praktikum Modul 2 ini kami diperintahkan untuk menjawab 17 soal mengenai DNS dan Webserver.

Luffy adalah seorang yang akan jadi Raja Bajak Laut. Demi membuat Luffy menjadi Raja Bajak Laut, Nami ingin membuat sebuah peta, bantu Nami untuk membuat peta berikut:

[![Whats-App-Image-2021-10-29-at-21-30-06.jpg](https://i.postimg.cc/1zFBM39b/Whats-App-Image-2021-10-29-at-21-30-06.jpg)](https://postimg.cc/hJSVtgQ0)

EniesLobby akan dijadikan sebagai DNS Master, Water7 akan dijadikan DNS Slave, dan Skypie akan digunakan sebagai Web Server. Terdapat 2 Client yaitu Loguetown, dan Alabasta.

Pada praktikum ini, kami membuat script yang bernama ```script.sh``` dan menjalankannya secara otomatis dengan cara menambahkan ```bash script.sh``` pada ```.bashrc```
### Soal 1
Semua node terhubung pada router Foosha, sehingga dapat mengakses internet.
Pertama-tama, kita harus menambahkan ```iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.205.0.0/16``` pada file ```.bashrc``` pada foosha. Bisa dilihat pada gambar dibawah ini:

[![Whats-App-Image-2021-10-29-at-21-59-33.jpg](https://i.postimg.cc/KvjFpddm/Whats-App-Image-2021-10-29-at-21-59-33.jpg)](https://postimg.cc/mhv0t6Ln)

Setelah itu, menambahkan IP DNS ke ```/etc/resolv.conf``` pada tiap node yang ada dengan menggunakan command ```echo nameserver 192.168.122.1 > /etc/resolv.conf``` yang dimasukkan pada file ```.bashrc``` sehingga bisa secara otomatis. Untuk mengecek apakah node sudah tersambung ke internet, kita bisa melakukan ping google, seperti pada contoh berikut :

[![Whats-App-Image-2021-10-30-at-00-03-43.jpg](https://i.postimg.cc/TY6wCrmT/Whats-App-Image-2021-10-30-at-00-03-43.jpg)](https://postimg.cc/rzfMpRQH)


### Soal 2
Luffy ingin menghubungi Franky yang berada di EniesLobby dengan denden mushi. Kalian diminta Luffy untuk membuat website utama dengan mengakses ```franky.yyy.com``` dengan alias ```www.franky.yyy.com``` pada folder kaizoku.
Pertama - tama kita melakukan instalasi bind dengan command ```apt-get install bind9 -y``` pada Enies Lobby, kemudian melakukan konfigurasi domain. Setelah itu kita membuat folder kaizoku dan copykan file db.local pada path /etc/bind ke dalam folder kazioku yang baru saja dibuat dan ubah namanya menjadi ```franky.E11.com```. 

[![Whats-App-Image-2021-10-30-at-00-11-12.jpg](https://i.postimg.cc/8PMyVVjh/Whats-App-Image-2021-10-30-at-00-11-12.jpg)](https://postimg.cc/xcjGKhGC)



### Soal 3
Setelah itu buat subdomain ```super.franky.yyy.com``` dengan alias ```www.super.franky.yyy.com``` yang diatur DNS nya di EniesLobby dan mengarah ke Skypie.
### Soal 4
Buat juga reverse domain untuk domain utama.
### Soal 5
Supaya tetap bisa menghubungi Franky jika server EniesLobby rusak, maka buat Water7 sebagai DNS Slave untuk domain utama.
### Soal 6
Setelah itu terdapat subdomain ```mecha.franky.yyy.com``` dengan alias ```www.mecha.franky.yyy.com``` yang didelegasikan dari EniesLobby ke Water7 dengan IP menuju ke Skypie dalam folder sunnygo.
### Soal 7
Untuk memperlancar komunikasi Luffy dan rekannya, dibuatkan subdomain melalui Water7 dengan nama ```general.mecha.franky.yyy.com``` dengan alias ```www.general.mecha.franky.yyy.com``` yang mengarah ke Skypie.
### Soal 8
Setelah melakukan konfigurasi server, maka dilakukan konfigurasi Webserver. Pertama dengan webserver ```www.franky.yyy.com```. Pertama, luffy membutuhkan webserver dengan DocumentRoot pada ```/var/www/franky.yyy.com```.
### Soal 9
Setelah itu, Luffy juga membutuhkan agar url ```www.franky.yyy.com/index.php/home``` dapat menjadi menjadi ```www.franky.yyy.com/home```. 
### Soal 10
Setelah itu, pada subdomain ```www.super.franky.yyy.com```, Luffy membutuhkan penyimpanan aset yang memiliki DocumentRoot pada ```/var/www/super.franky.yyy.com```
### Soal 11
Akan tetapi, pada folder /public, Luffy ingin hanya dapat melakukan directory listing saja.
### Soal 12
Tidak hanya itu, Luffy juga menyiapkan error file 404.html pada folder /error untuk mengganti error kode pada apache . 
