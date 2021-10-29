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

Kemudian, kita mengedit file ```franky.E11.com``` dan melakukan restart pada bind9, seperti pada gambar berikut :

[![Whats-App-Image-2021-10-30-at-00-15-55.jpg](https://i.postimg.cc/kXT2G269/Whats-App-Image-2021-10-30-at-00-15-55.jpg)](https://postimg.cc/ykS1rYyr)

Untuk mengecek apakah sudah benar, kita bisa mengecek lewat node Loguetown dengan melakukan setting nameserver : ```echo nameserver 192.205.2.2 > /etc/resolv.conf``` dan melakukan ```ping franky.E11.com``` yang seharusnya mengarah ke IP EniesLobby dan untuk mengecek alias bisa menggunakan ```host -t CNAME www.franky.E11.com``` seperti pada gambar :

[![Whats-App-Image-2021-10-30-at-00-23-47.jpg](https://i.postimg.cc/P5hngyr5/Whats-App-Image-2021-10-30-at-00-23-47.jpg)](https://postimg.cc/mtdnMQHv)

### Soal 3
Setelah itu buat subdomain ```super.franky.yyy.com``` dengan alias ```www.super.franky.yyy.com``` yang diatur DNS nya di EniesLobby dan mengarah ke Skypie.
Untuk membuat subdomain, kita akan meng-edit file ```franky.E11.com``` pada EniesLobby dan menambahkan konfigurasinya setelah itu melakukan restart bind 9 seperti gambar berikut :

[![Whats-App-Image-2021-10-30-at-00-31-29.jpg](https://i.postimg.cc/vHCcfpzS/Whats-App-Image-2021-10-30-at-00-31-29.jpg)](https://postimg.cc/jLQxr3Bz)

Untuk mengecek apakah sudah benar atau belum, kita bisa melakukan ping dengan command ```ping super.franky.E11.com``` pada Loguetown dan hasilnya akan mengarah ke IP Skypie.

[![Whats-App-Image-2021-10-30-at-00-34-56.jpg](https://i.postimg.cc/ry0jSt2V/Whats-App-Image-2021-10-30-at-00-34-56.jpg)](https://postimg.cc/V5wXwvNp)

### Soal 4
Buat juga reverse domain untuk domain utama.
Untuk membuat reverse domain, pertama - tama kita akan mengedit file ```/etc/bind/named.conf.local``` pada EniesLobby dengan menambahkan konfigurasi zone reverse DNS. Kemudian copy file db.local pada path ```/etc/bind``` ke dalam folder jarkom yang baru saja dibuat dan ubah namanya menjadi ```2.205.192.in-addr.arpa```

[![Whats-App-Image-2021-10-30-at-00-38-31.jpg](https://i.postimg.cc/ZKX18hMg/Whats-App-Image-2021-10-30-at-00-38-31.jpg)](https://postimg.cc/Wh6WVxj6)

Setelah itu, edit file ```2.205.192.in-addr.arpa``` menjadi seperti gambar di bawah ini :

[![Whats-App-Image-2021-10-30-at-00-45-33.jpg](https://i.postimg.cc/k4tjXVng/Whats-App-Image-2021-10-30-at-00-45-33.jpg)](https://postimg.cc/gXmyg2XC)

Dan setelah itu melakukan restart bind9. Untuk mengecek apakah sudah benar, kita bisa mengecek pada Loguetown dengan command ```host -t PTR 192.205.2.2```

[![Whats-App-Image-2021-10-30-at-00-49-02.jpg](https://i.postimg.cc/TYHWQtVB/Whats-App-Image-2021-10-30-at-00-49-02.jpg)](https://postimg.cc/nCBzhYw1)

### Soal 5
Supaya tetap bisa menghubungi Franky jika server EniesLobby rusak, maka buat Water7 sebagai DNS Slave untuk domain utama.
Untuk membuat DNS Slave, pertama kita akan mengedit zone "franky.e11.com" pada ```/etc/bind/named.conf.local``` menjadi sebagai berikut :

[![Whats-App-Image-2021-10-30-at-00-53-41.jpg](https://i.postimg.cc/m2xrrKSL/Whats-App-Image-2021-10-30-at-00-53-41.jpg)](https://postimg.cc/fkKs22Fp)

Kemudian kita lakukan restart bind9.
Pada Water 7, kita akan menginstall bind9 dan mengedit file ```/etc/bind/named.conf.local``` dan mengisinya menjadi :

[![Whats-App-Image-2021-10-30-at-00-58-22.jpg](https://i.postimg.cc/4xG4ZtQB/Whats-App-Image-2021-10-30-at-00-58-22.jpg)](https://postimg.cc/56PWSXGC)

Setelah itu, kita melakukan restart pada bind9.

Untuk mengecek apakah sudah benar, maka kita akan stop bind9 pada EniesLobby, selanjutnya kita tambahkan IP Water 7 ke ```/etc/resolv.conf``` pada Loguetown dengan command ```echo 'nameserver 192.205.2.3' >> /etc/resolv.conf```. Setelah itu kita coba ping franky.e11.com dan seharusnya tetap berhasil walau service bind9 pada EniesLobby di stop.

[![Whats-App-Image-2021-10-30-at-01-07-15.jpg](https://i.postimg.cc/28sbWVFZ/Whats-App-Image-2021-10-30-at-01-07-15.jpg)](https://postimg.cc/qzGvVBFJ)

### Soal 6
Setelah itu terdapat subdomain ```mecha.franky.yyy.com``` dengan alias ```www.mecha.franky.yyy.com``` yang didelegasikan dari EniesLobby ke Water7 dengan IP menuju ke Skypie dalam folder sunnygo.

Untuk membuat subdomain dengan delegasi, pertama kita akan mengedit file ```/etc/bind/kaizoku/franky.e11.com``` menjadi sebagai berikut :

[![Whats-App-Image-2021-10-30-at-01-13-23.jpg](https://i.postimg.cc/vHgXMxZg/Whats-App-Image-2021-10-30-at-01-13-23.jpg)](https://postimg.cc/GHRvx2Yd)

Kemudian edit file ```/etc/bind/named.conf.options``` pada EniesLobby dengan comment dnssec-validation auto; dan tambahkan baris ```allow-query{any;};``` pada ```/etc/bind/named.conf.options.```

[![Whats-App-Image-2021-10-30-at-01-17-02.jpg](https://i.postimg.cc/26Y8jWYz/Whats-App-Image-2021-10-30-at-01-17-02.jpg)](https://postimg.cc/t1rH2Y7f)

Setelah itu kita lakukan restart pada service bind9.

Setelah melakukan konfigurasi pada EniesLobby, kita akan melakukan konfigurasi pada Water 7.

Pada Water 7 kita akan mengedit file ```/etc/bind/named.conf.options``` dengan comment dnssec-validation auto; dan tambahkan baris ```allow-query{any;};``` pada ```/etc/bind/named.conf.options.```

Lalu edit file ```/etc/bind/named.conf.local.```

Kemudian buat direktori dengan nama delegasi yaitu sunnygo dan copy db.local ke direktori sunnygo dan edit namanya menjadi ```mecha.franky.e11.com.```

[![Whats-App-Image-2021-10-30-at-01-28-35.jpg](https://i.postimg.cc/DwDRc3pH/Whats-App-Image-2021-10-30-at-01-28-35.jpg)](https://postimg.cc/rD1h83kN)

Kemudian kita edit file ```mecha.franky.e11.com``` menjadi :

[![Whats-App-Image-2021-10-30-at-01-37-03.jpg](https://i.postimg.cc/tgvtLFVM/Whats-App-Image-2021-10-30-at-01-37-03.jpg)](https://postimg.cc/Z93dNBH8)

Kemudian lakukan restart pada service bind9.

Untuk melakukan testing apakah sudah benar, kita bisa melakukan ping ```mecha.franky.e11.com``` pada client Loguetown dan harusnya akan mengarah ke IP Skypie.

[![Whats-App-Image-2021-10-30-at-01-43-07.jpg](https://i.postimg.cc/T1N6b7yc/Whats-App-Image-2021-10-30-at-01-43-07.jpg)](https://postimg.cc/dZCpP9j7)

### Soal 7
Untuk memperlancar komunikasi Luffy dan rekannya, dibuatkan subdomain melalui Water7 dengan nama ```general.mecha.franky.yyy.com``` dengan alias ```www.general.mecha.franky.yyy.com``` yang mengarah ke Skypie.

Untuk menambahkan subdomain, kita bisa lakukan dengan mengedit file ```/etc/bind/sunnygo/mecha.franky.e11.com``` menjadi :

[![Whats-App-Image-2021-10-30-at-01-32-25.jpg](https://i.postimg.cc/Mpky0sbt/Whats-App-Image-2021-10-30-at-01-32-25.jpg)](https://postimg.cc/7fVGwnRT)



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
