# Modul 1 - Virtualisasi

## Virtualisasi

**Virtualisasi** merupakan upaya untuk  menghasilkan suatu bentuk virtual dari sesuatu yang bersifat fisik. Hal  ini bisa berupa perangkat penyimpanan data maupun sistem operasi,  termasuk juga pembuatan sumber daya tunggal seperti server. Jenis  virtualisasi pun ada banyak, seperti perangkat keras, perangkat lunak,  jaringan, data, dan memori. Istilah virtualisasi ini ternyata sudah dipakai sejak tahun 1960-an. Namun karena teknologi *cloud* belum *booming* seperti sekarang, maka istilah ini pun juga belum seberapa dikenal kala itu.

Menurut [Microsoft](https://azure.microsoft.com/en-us/overview/what-is-virtualization/), virtualisasi adalah cara membuat sebuah komputer fisik atau sebuah *server* menjadi beberapa mesin virtual yang mampu berinteraksi secara independen. Bahkan, mesin virtual ini bisa dijalankan menggunakan sistem operasi atau aplikasi yang berbeda meskipun menggunakan satu *host machine* atau perangkat yang sama.

### Manfaat Virtualisasi

1. Efisiensi Biaya

   Virtualisasi mengurangi jumlah *server* yang dijalankan. Itu artinya menghemat biaya *hardware* dan juga jumlah total energi yang harus dijalankan. Satu server bisa  dibagi resourcenya menjadi seolah-olah beberapa server yang bisa  menjalankan tugas sendiri-sendiri.

2. Efisiensi Sumber Daya

   Tanpa Virtualisasi, setiap *server* aplikasi membutuhkan CPU fisiknya masing-masing. Tentunya, hal ini diharuskan untuk membeli *server* terpisah untuk setiap aplikasi yang ingin dijalankan. Nah, dengan virtualisasi, maka kita dapat memaksimalkan kapasitas penggunaan setiap satu perangkat keras.

3. Manajemen yang sederhana

   Lebih sedikit sumber daya fisik menghasilkan lebih sedikit waktu yang  dihabiskan untuk mengelola dan memelihara server. Tugas yang dapat  memakan waktu berhari-hari atau berminggu-minggu di lingkungan fisik  dapat dilakukan dalam hitungan menit.

4. *Eco Friendly*

   Mengurangi *server* dapat diasumsikan mengurangi panas yang dihasilkan pada suatu ruangan server atau *data center*.

### Tipe Virtualisasi

Ada enam tipe virtualisasi :

1. Virtualisasi jaringan adalah metode menggabungkan sumber daya yang tersedia dalam jaringan dengan memecah bandwidth yang tersedia menjadi  saluran, yang masing-masing independen dari yang lain dan dapat  ditugaskan – atau dipindahkan – ke server atau perangkat tertentu secara real time.

2. Virtualisasi penyimpanan adalah penyatuan penyimpanan fisik dari  beberapa perangkat penyimpanan jaringan ke dalam apa yang tampak sebagai perangkat penyimpanan tunggal yang dikelola dari konsol pusat.

3. Virtualisasi server adalah penyembunyian sumber daya server –  termasuk jumlah dan identitas masing-masing server fisik, prosesor dan  sistem operasi – dari pengguna server.

4. Virtualisasi data adalah meringkas rincian teknis data dan  manajemen data, seperti lokasi, kinerja atau format, yang mendukung  akses yang lebih luas dan ketahanan lebih banyak yang terkait dengan  kebutuhan bisnis.

5. Virtualisasi desktop adalah virtualisasi beban workstation  daripada server. Ini memungkinkan user untuk mengakses atau meremote  desktop dari jarak jauh.

6. Virtualisasi aplikasi memisahkan lapisan aplikasi dari sistem  operasi. Dengan cara ini, aplikasi dapat berjalan dalam bentuk  enkapsulasi tanpa bergantung pada sistem operasi di bawahnya.

### Cara Kerja Virtualisasi

Penggunaan utama teknologi virtualisasi adalah virtualisasi server,  yang menggunakan lapisan perangkat lunak yang disebut hypervisor untuk  meniru perangkat keras yang mendasarinya. Hypervisor mengambil sumber  daya fisik dan memisahkannya sehingga dapat dimanfaatkan oleh virtual  environment. Mereka dapat berjalan di atas OS atau mereka dapat langsung diinstal ke perangkat keras.

![VIRTUALISASI](assets\VIRTUALISASI.jpg)

Proses virtualisasi mengikuti langkah-langkah yang tercantum di bawah ini:

1. Hypervisor melepaskan sumber daya fisik dari lingkungan fisik mereka.
2. Sumber daya diambil dan dibagi, sesuai kebutuhan, dari lingkungan fisik ke berbagai lingkungan virtual.
3. User sistem bekerja dengan melakukan perhitungan dalam lingkungan virtual.
4. Setelah lingkungan virtual berjalan, user atau program dapat  mengirim instruksi yang membutuhkan sumber daya tambahan dari lingkungan fisik. Sebagai tanggapan, hypervisor menyampaikan pesan ke sistem fisik dan menyimpan perubahan. Proses ini akan terjadi pada kecepatan asli.

Lingkungan virtual sering disebut sebagai mesin tamu (guest machine)  atau mesin virtual (virtual machine). VM bertindak seperti file data  tunggal yang dapat ditransfer dari satu komputer ke komputer lain dan  dibuka di keduanya.

## Virtual Machine

*Virtual machine* (VM) adalah sebuah emulasi dari sebuah sistem komputer. Secara sederhana, *virtual machine* membuat kita bisa membagi *resource hardware* dari satu *hardware* fisik menjadi beberapa sistem komputer. 

Sebagai contoh, kita memiliki satu PC yang memiliki prosesor dengan 4 *core*, RAM sebesar 8 GB serta *harddisk* 500GB misalnya. Tanpa VM tentu kita hanya bisa menginstall 1 OS atau  beberapa OS tapi tak bisa berjalan bersamaan. Dengan VM, kita bisa  membagi sistem komputer menjadi dua masing-masing memiliki prosesor 2  core,  RAM 4GB, serta harddisk 250GB dan tentu saja pembagian *resource hardware* tidak harus sama rata. Dengan ini, maka kita dapat menginstall OS di  setiap sistem komputer dan dapat menjalankannya secara bersamaan  sehingga kita seolah memiliki 2 PC yang berbeda.

Teknologi ini sering digunakan untuk  server dan memunculkan istilah Virtual Private Server (VPS) tapi sedikit pula digunakan oleh *app developer* karena project yang sedang dikerjakannya memiliki platform yang berbeda dengan platform yang dimiliki.

## Container

Berbeda dari VM, *container* adalah sebuah virtualisasi OS yang dapat membungkus suatu aplikasi beserta *dependency* dan *environment*-nya. Setiap *container* ini memiliki process yang terisolir sehingga tidak mengganggu host OS ataupun container yang lain. Prinsip *container* ini mirip dengan kontainer yang ada di kapal kargo di mana kapal kargo tersebut diibaratkan sebagai sistem komputer.

Jika dibandingkan dengan VM, secara pengaturan kontainer lebih mudah. Hal ini disebabkan karena konsep berbagi *resource hardware* dari *container* lebih fleksibel bila dibandingkan VM. Sebagai contoh, tadi disebutkan  bahwa kita mempunyai 1 PC dengan 4 Core, RAM 8 GB, dan storage sebesar  500GB. Katakanlah kita mempunyai 2 *container* dengan kebutuhan RAM berbeda. Beberapa apps dalam *container* A membutuhkan RAM 5GB sedangkan *apps* dalam *container* B membutuhkan RAM 2GB. Dengan *container*, kita tak perlu menset kebutuhan *hardware resource* setiap *container* karena berada dalam satu sistem komputer. Sementara jika kita memakai VM dengan *hardware resource* yang sudah kita bagi sama rata seperti disebutkan di contoh sebelumnya, kita tidak mungkin memasang apps di container A di salah satu sistem  komputer karena RAM maksimal yang bisa kita pakai hanyalah 4GB.

Faktor portabilitas juga menjadi kelebihan yang dimiliki oleh *container*. Para *developer* bisa membagikan *container* dengan format ISO image ke setiap perangkat yang dia pakai ataupun ke *developer* lain.

### Linux Container

Platform ini merupakan cikal bakal  lahirnya container. Linux Containers (LXC) ini adalah virtualisasi OS  yang memungkinkan kita menjalankan beberapa sistem Linux di dalam satu  sistem komputer secara bersamaan. Tentu saja platform ini hanya berlaku  untuk Linux saja.

## Virtual Machine vs Container

| **Virtual Machine**                                      | **Container**                                    |
| -------------------------------------------------------- | ------------------------------------------------ |
| Berat                                                    | Ringan                                           |
| Performa terbatas pada konfigurasi VM                    | Performa maksimum tergantung pada hardware fisik |
| Virtualisasi pada level hardware                         | Virtualisasi pada level OS                       |
| Waktu start up dalam hitungan menit                      | Waktu start up dalam hitungan detik              |
| Terisolasi penuh pada level hardware sehingga lebih aman | Terisolasi pada level proses                     |

## Instalasi

- Persiapan *Server host*

  ```bash
  sudo apt install -y build-essential linux-headers-$(uname -r)
  ```

  On the VM window, go to **Devices** » **Insert Guest Additions CD Image**, and install it:

  ```bash
  sudo mount /dev/cdrom /media
  cd /media
  sudo bash VBoxLinuxAdditions.run
  ```

  Mengganti *sources list* ubuntu

  ```bash
  sudo nano /etc/apt/sources.list
  ```

  menjadi

  ```ini
  deb http://archive.ubuntu.com/ubuntu/ focal main restricted universe multiverse
  deb-src http://archive.ubuntu.com/ubuntu/ focal main restricted universe multiverse
  
  deb http://archive.ubuntu.com/ubuntu/ focal-updates main restricted universe multiverse
  deb-src http://archive.ubuntu.com/ubuntu/ focal-updates main restricted universe multiverse
  
  deb http://archive.ubuntu.com/ubuntu/ focal-security main restricted universe multiverse
  deb-src http://archive.ubuntu.com/ubuntu/ focal-security main restricted universe multiverse
  
  deb http://archive.ubuntu.com/ubuntu/ focal-backports main restricted universe multiverse
  deb-src http://archive.ubuntu.com/ubuntu/ focal-backports main restricted universe multiverse
  
  deb http://archive.canonical.com/ubuntu focal partner
  deb-src http://archive.canonical.com/ubuntu focal partner
  ```

  ![edit-source-list](assets\edit-source-list.png)

  ```
  sudo apt update; sudo apt upgrade -y
  ```

  

- Install lxc 

  ```bash
  sudo apt-get install lxc lxctl lxc-templates net-tools
  ```

- Check Konfigurasi

  ```bash
  sudo lxc-checkconfig
  ```

- Menampilkan template container yang tersedia

  ```bash
  sudo ls /usr/share/lxc/templates/
  ```

  hasilnya :

  ![show-templates](assets\show-templates.png)

- Membuat container Ubuntu

  Syntax Command :

  ```bash
  sudo lxc-create -n namakontainer -t template
  ```

  Sehingga :

  ```bash
  sudo lxc-create -n server1_ubuntu -t ubuntu
  ```

  ![instalasi-lxc](assets\instalasi-lxc.png)

- Menjalankan container

  ```bash
  sudo lxc-start -n server1_ubuntu -d
  ```

- Masuk Ke console container

  ```bash
  sudo lxc-console -n server1_ubuntu
  ```

  coba untuk menjalankan update, dan upgrade, apakah sudah terhubung dengan internet?

  ```bash
  sudo apt update; sudo apt upgrade -y
  ```

  ![console-test](assets\console-test.png)

  Untuk keluar dari lxc-console, tekan **ctrl + a**, selanjutnya tekan **q**

- Membuat container kedua

  ```bash
  sudo lxc-create -n server2_ubuntu -t ubuntu
  ```
  
- Menampilkan container yang tersedia

  ```bash
  sudo lxc-ls	-f
  ```

  ![lxc-ls](assets\lxc-ls.png)

- Menampilkan informasi dari sebuah container

  ```bash
  sudo lxc-info -n server1_ubuntu
  ```

  ![lxc-info](assets\lxc-info.png)

- Menampilkan alamat IP container

  ```bash
  sudo lxc-ls --fancy server1_ubuntu
  ```

  ![lxc-fancy](assets\lxc-fancy.png)

- Menghentikan container

  ```bash
  sudo lxc-stop -n server1_ubuntu
  ```

- Menghapus container

  ```bash
  sudo lxc-destroy server2_ubuntu	
  ```

  ![lxc-destroy](assets\lxc-destroy.png)



## Referensi

- https://blog.lintasarta.net/article/virtualisasi-pengertian-dan-bagaimana-anda-dapat-memanfaatkannya
- https://indonesiancloud.com/apa-itu-virtualisasi/
- https://glints.com/id/lowongan/virtualization-adalah/#.YWG2GH0xWUk
- http://nguprek.com/apa-itu-virtualisasi/
- https://inixindojogja.co.id/container-vs-virtual-machine/

## Soal Latihan Praktikum

1. Buat 2 LXC dengan nama ubuntu_php5.6 (dengan ubuntu 16.04) dan ubuntu_php7.4 (dengan ubuntu 18.04)

   ```bash
   hint:
   sudo lxc-create -n ubuntu_php5.6 -t download -- --dist ubuntu --release xenial --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
   ```

   hint: gunakana lxc-attach daripada lxc-console

2. install nginx dan nginx-extras di masing masing lxc

   ```bash
   hint:
   sudo apt install nginx nginx-extras
   ```

   

3. proxy server dari vm ke lxc 1 dan 2

   ```
   hint:
   gunakan proxy_pass, set static ip dulu ke masing masing lxc
   ```

   

   

   