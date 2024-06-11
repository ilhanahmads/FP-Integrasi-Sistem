# Final Project Integrasi Sistem
Dokumentasi pengerjaan Final Project Mata Kuliah Integrasi Sistem 2024 Kelompok 6 Kelas A

## Anggota Kelompok
| Nama               | NRP         |
| ------------------ | ----------- |
| Iki Adfi Nur Mohamad   | 5027221033  |
| Ilhan Ahmad Syafa  | 5027221040  |

## *Project* 1
### 1. *Setup* *Hardware*
Pertama-tama, lakukan *setup* untuk *hardware* yang diperlukan seperti NodeMCU esp8266, sensor DHT22 dan kabel jumper. Pastikan semua kabel terpasang dengan baik. Berikut merupakan *mapping* kabel dari *hardware* yang kami gunakan:

| Pin Perangkat | Koneksi    | Deskripsi               |
| ------------- | ---------- | ----------------------- |
| VCC           | 3.3 V      | Tegangan suplai 3.3V    |
| Data (+)      | D1 / GPIO5 | Pin data untuk GPIO5    |
| GND (-)       | GND        | Ground (tanah)          |

<a href="https://imgbb.com/"><img src="https://i.ibb.co.com/Cs4Thp7/Foto-Alat.jpg" alt="Foto-Alat" border="0"></a> <br>

### 2. *Setup* Arduino IDE
Kemudian, tancapkan NodeMCU esp8266 ke laptop untuk mulai memprogram. Pertama, *install* *library* yang diperlukan seperti *library* DHT22 dan PubSub (agar *server* MQTT dapat melakukan *publish* dan *subscribe* melalui *broker*). Kedua, konfigurasi program yang akan di*upload* ke NodeMCU esp8266. Di sini kami ambil *resource*-nya dari *course* *Udemy* yang telah disediakan dengan menyesuaikan beberapa konfigurasi sesuai dengan kelompok kami seperti koneksi WiFi, *server*/IP *broker* MQTT, *topic*, *authorisasi* (username & password) serta pin yang digunakan. Setelah itu, *upload* program dan buka *serial monitor* sesuai *baud rate* (kami menggunakan 115200). Dapat terlihat bahwa *output* hasil pengukuran dari sensor akan muncul.

<a href="https://ibb.co.com/qWkgdVH"><img src="https://i.ibb.co.com/rc4pmNB/Install-DHT-Library.png" alt="Install-DHT-Library" border="0"></a>
<a href="https://ibb.co.com/L0DT9Gg"><img src="https://i.ibb.co.com/hgxG2qd/Install-Pub-Sub-Library.png" alt="Install-Pub-Sub-Library" border="0"></a>
<a href="https://ibb.co.com/7ktdPCR"><img src="https://i.ibb.co.com/8YgLqsd/Screenshot-2024-06-11-125404.png" alt="Screenshot-2024-06-11-125404" border="0"></a>
<a href="https://ibb.co.com/HDw55v4"><img src="https://i.ibb.co.com/PZXqqpj/Screenshot-2024-06-11-125444.png" alt="Screenshot-2024-06-11-125444" border="0"></a>

### 3. *Setup* *Dashboard* HTML
Ketiga, konfigurasi HTML untuk menampilkan data yang didapatkan dari sensor DHT22. Kami mendapatkan *resource*-nya dari *course* *Udemy* dengan menyesuaikan beberapa konfigurasi sesuai dengan program sebelumnya yaitu mengganti IP *broker*, port, *topic*, username dan password (kalau ada). Jika sudah berhasil, maka tampilan *dashboard* HTML akan menjadi seperti gambar di bawah ini.

<a href="https://ibb.co.com/gPy7CFv"><img src="https://i.ibb.co.com/RB2SW4h/Screenshot-2024-06-11-125731.png" alt="Screenshot-2024-06-11-125731" border="0"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co.com/M97Sj1z/Screenshot-2024-06-11-130137.png" alt="Screenshot-2024-06-11-130137" border="0"></a>

### 4. *Testing* melalui [mqtt.run](http://mqtt.run)
Kita juga dapat memonitor *output* melalui website [mqtt.run](http://mqtt.run) seperti gambar di bawah ini dengan memasukkan konfigurasi yang sesuai dengan program di arduino. Jika sudah berhasil, seharusnya *output* yang ditampilkan di website [mqtt.run](http://mqtt.run) dan *dashboard* HTML sama persis karena mem*fetch* dari sumber yang sama.

![image](https://github.com/ilhanahmads/FP-Integrasi-Sistem/assets/127307991/08060401-ed3c-499f-b679-2a568f8fdf8d)
<a href="https://imgbb.com/"><img src="https://i.ibb.co.com/M97Sj1z/Screenshot-2024-06-11-130137.png" alt="Screenshot-2024-06-11-130137" border="0"></a>

## *Project* 2
Sebelum melanjutkan ke *setup* *project* 2, pastikan *setup* pada *project* 1 telah selesai dan berjalan lancar.

### 1. *Setup* LED Blink
Pertama-tama, lakukan *setup* untuk menyalakan LED. LED ini berfungsi sebagai indikator bahwa suhu terdeteksi oleh sensor. Kami menggunakan pin GPIO yang sama seperti di *course*, sehingga hanya perlu menyesuaikan pemasangan kabel jumper pada *board* LED-nya sesuai pin GPIO yaitu 12. <br><br>
![image](https://github.com/ilhanahmads/FP-Integrasi-Sistem/assets/127307991/90ba34c6-60a4-43c8-a389-8f320cf98fc8) <br>

Berikut ini merupakan rangkaian LED dan Raspberry <br><br>
![image](https://github.com/ilhanahmads/FP-Integrasi-Sistem/assets/127307991/a79bc6f9-f88a-4456-834d-0e8e904d8239)

### 2. *Setup* Mosquito *Subscription*
Masukkan kode pada *resources* yang sudah disediakan dalam file bernama `mqtt_sub.py` dengan *command* `sudo nano mqtt_sub.py`
- `pip install paho-mqtt`
- *Setup* GPIO *output*, pastikan sama dengan rangkaian LED dan *setup* *blink* sebelumnya, yaitu di GPIO 12
- Tentukan *topic* *client subscribe* pada fungsi `on_connect`. *Topic* kami adalah `/kel6/room/led`
- Pada fungsi `client.username_pw_set`, pastikan sama dengan *setup broker* sebelumnya. Kami sengaja mengosongkan username & password pada *broker*.
- Pada fungsi `client.connect` masukkan IP *Broker*, PORT, dan waktu *looping*. Konfigurasi kelompok kami: `(“167.172.87.186”, 1883, 60)` <br><br>
![image](https://github.com/ilhanahmads/FP-Integrasi-Sistem/assets/127307991/a69d3535-665d-419a-8f42-d59242ab7deb)

### 3. *Setup* *Dashboard* HTML
Pastikan LED telah dimatikan terlebih dahulu. Kemudian kita konfigurasikan *source code webpage* yang ada pada *resource* *course project* 2. Pastikan MQTT *Settings* sudah benar dan sesuai dengan IP *Broker* yang digunakan pada file `mqtt_sub.py` sebelumnya. <br><br>

![image](https://github.com/ilhanahmads/FP-Integrasi-Sistem/assets/127307991/e5be09f8-7fb6-4ae9-98ca-6866da25c6fd) <br><br>

Tambahkan fungsi untuk melakukan konfigurasi pada LED <br><br>
![image](https://github.com/ilhanahmads/FP-Integrasi-Sistem/assets/127307991/2f6cc287-0e75-47b1-b399-b6e6b542359b) <br><br>

Tambahkan fungsi untuk memberikan pesan bahwa LED telah menyala atau mati <br><br>
![image](https://github.com/ilhanahmads/FP-Integrasi-Sistem/assets/127307991/286b57a1-c1c4-449d-b2e5-23f9d311dffe) <br><br>

Tampilan *Dashboard* <br><br>
![image](https://github.com/ilhanahmads/FP-Integrasi-Sistem/assets/127307991/abf162eb-17f2-41db-be2a-814b830c4aa8)

### *Testing*
[Video *Testing*]

### 4. *Setup* *Threshold*
Masukkan kode pada *resources* yang sudah disediakan dalam file bernama `mqtt_pub.py` dengan *command* `sudo nano mqtt_pub.py`.
- Konfigurasikan `client.subscribe` dengan topik yang sesuai yaitu ``/kel6/room/temperature``
- Pada fungsi JSON untuk cek temperatur. Kami mengatur *threshold*-nya di atas 1 celcius, maka lampu akan menyala
- Tentukan pesan pada fungsi `temperature`, tepatnya di `client.publish` dengan menggunakan ``“/kel6/room/led”, “On”``
- Pada fungsi yang sama juga, tentukan pesan untuk kondisi `else` dengan menggunakan ``“/kel6/room/led”, “Off”``
- Pada fungsi `client.connect` masukkan IP *Broker*, PORT, dan waktu *looping*. Konfigurasi kelompok kami: `(“167.172.87.186”, 1883, 60)` <br><br>
![image](https://github.com/ilhanahmads/FP-Integrasi-Sistem/assets/127307991/21ac359e-409d-4ed8-89ee-765645273f04)

### *Testing*
Jalankan kode pada Raspberry Pi dengan *command* `python mqtt_pub.py`. <br><br>
![image](https://github.com/ilhanahmads/FP-Integrasi-Sistem/assets/127307991/644877f1-a44b-4ace-845f-c2f8efa04e0f) <br><br>

Jalankan kode pada Raspberry Pi dengan *command* `python mqtt_sub.py`. <br><br>
![image](https://github.com/ilhanahmads/FP-Integrasi-Sistem/assets/127307991/f6cf4f88-37c9-4771-bf12-115690ea757f)


