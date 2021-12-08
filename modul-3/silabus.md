# Modul 3 - DNS, & Load Balancer

## DNS (*Domain Name Server*)
### Pengertian
DNS (Domain Name System) adalah sistem penamaan untuk semua device (smartphone, computer, atau network) yang terhubung dengan internet. DNS Server berfungsi menerjemahkan nama domain menjadi alamat IP. DNS dibuat guna untuk menggantikan sistem penggunaan file host yang dirasa tidak efisien.
### Cara Kerja
![Cara Kerja DNS](assets/cara-kerja.jpg)
Client akan meminta alamt IP dari suatu domain ke DNS server. Jika pada DNS server data alamat IP dari DNS server tersebut ada maka akan di return alamat IP nya kembali menuju client. Jika DNS server tersebut tidak memiliki alamat IP dari domain tersebut maka dia akan bertanya kepada DNS server yang lain sampai alamat domain itu ditemukan.	
### Aplikasi DNS Server
aplikasi BIND9 sebagai DNS server, karena BIND(Berkley Internet Naming Daemon) adalah DNS server yang paling banyak digunakan dan juga memiliki fitur-fitur yang cukup lengkap.
### List DNS Record
| Tipe          | Deskripsi                     |
| ------------- |:-----------------------------|
| A             | Memetakan nama domain ke alamat IP (IPv4) dari komputer hosting domain|
| AAAA          | AAAA record hampir mirip A record, tapi mengarahkan domain ke alamat Ipv6|
| CNAME         | Alias ​​dari satu nama ke nama lain: pencarian DNS akan dilanjutkan dengan mencoba lagi pencarian dengan nama baru|
| NS            | Delegasikan zona DNS untuk menggunakan authoritative name servers yang diberikan|
| PTR           | Digunakan untuk Reverse DNS (Domain Name System) lookup|
| SOA           | Mengacu server DNS yang mengediakan otorisasi informasi tentang sebuah domain Internet|
| TXT           | Mengijinkan administrator untuk memasukan data acak ke dalam catatan DNS, catatan ini juga digunakan di spesifikasi Sender Policy Framework|
### SOA (Start of Authority)
Adalah informasi yang dimiliki oleh suatu DNS zone.

| Nama          | Deskripsi                     |
| ------------- |:-----------------------------|
| Serial        | Jumlah revisi dari file zona ini. Kenaikan nomor ini setiap kali file zone diubah sehingga perubahannya akan didistribusikan ke server DNS sekunder manapun|
| Refresh       | Jumlah waktu dalam detik bahwa nameserver sekunder harus menunggu untuk memeriksa salinan baru dari zona DNS dari nameserver utama domain. Jika file zona telah berubah maka server DNS sekunder akan memperbarui salinan zona tersebut agar sesuai dengan zona server DNS utama|
| Retry         | Jumlah waktu dalam hitungan detik bahwa nameserver utama domain (atau server) harus menunggu jika upaya refresh oleh nameserver sekunder gagal sebelum mencoba refresh zona domain dengan nameserver sekunder itu lagi|
| Expire        | Jumlah waktu dalam hitungan detik bahwa nameserver sekunder (atau server) akan menahan zona sebelum tidak lagi mempunyai otoritas|
| Minimum       | Jumlah waktu dalam hitungan detik bahwa catatan sumber daya domain valid. Ini juga dikenal sebagai TTL minimum, dan dapat diganti oleh TTL catatan sumber daya individu|
| TTL           | (waktu untuk tinggal) - Jumlah detik nama domain di-cache secara lokal sebelum kadaluarsa dan kembali ke nameserver otoritatif untuk informasi terbaru|

### Latihan
#### Persiapan Konfigurasi
1. Hapus hosts vm.local dari hostfile windows
	![host windows](assets/host-windows.png)
2. Buka Ubuntu VM, pastikan network menggunakan bridge network
3. Tambahkan konfigurasi nginx untuk virtual hosts vm.local
	![Nginx VM local](assets/nginx-vm.local.png)
4. Edit etc/hosts
	![Konfigurasi hosts](assets/etc-hosts.png)
5. Restart nginx
	```bash
	sudo service nginx restart
	```
6. Check Konfigurasi
	```bash
	curl -i http://vm.local
	curl -i http://www.wm.local
	```
7. Catat IP VM
	```bash
	ip addr show enp0s3
	```
	![ip addr show](assets/ip-addr-show.png)
	
	kita catat bahwa IP VM kita adalah 172.20.10.4	

#### Instalasi DNS Master
DNS master adalah DNS utama yang akan digunakan sebagai penerjemah alamat domain menjadi alamat ip. untuk instalasi, silahkan buka ubuntu VM. DNS Master menggunakan aplikasi bind9, untuk langkah instalasi hanya perlu menuliskan
```bash
sudo apt install bind9
```
![Ubuntu 20 Install Bind9](assets/ubuntu20-install-bind9.png)

#### Konfigurasi DNS Master
1. Pembuatan Domain
	- Lakukan perintah untuk merubah konfigurasi bind9 seperti dibawah ini
		```bash
		sudo nano /etc/bind/named.conf.local
		```
	- Daftarkan domain vm.local
		```bash
		zone "vm.local" {
			type master;
			file "/etc/bind/vm/vm.local";
		};
		```
		![named conf local](assets/named-conf-local.png)
	- Buat folder vm di dalam /etc/bind
		```bash
		sudo mkdir /etc/bind/vm
		```
	- Copykan file db.local pada path /etc/bind ke dalam folder vm yang baru saja dibuat dan ubah namanya menjadi vm.local
		```bash
		sudo cp /etc/bind/db.local /etc/bind/vm/vm.local
		```
	- Kemudian buka file vm.local dan edit seperti gambar berikut dengan IP ubuntu VM masing-masing kelompok:
	- 
		![](assets/vmlocal-conf.png)
	- Restart bind9 dengan perintah
		```bash
		sudo service bind9 restart
		```
2. Reverse DNS (Record PTR)

	Jika pada pembuatan domain sebelumnya DNS server kita bekerja menerjemahkan string domain vm.local kedalam alamat IP agar dapat dibuka, maka Reverse DNS atau Record PTR digunakan untuk menerjemahkan alamat IP ke alamat domain yang sudah diterjemahkan sebelumnya.
	- Edit file /etc/bind/named.conf.local pada wsl
		```bash
		sudo nano /etc/bind/named.conf.local
		```
	- Lalu tambahkan konfigurasi berikut ke dalam file named.conf.local
		```bash
		zone "10.20.172.in-addr.arpa" {
		    type master;
		    file "/etc/bind/vm/100.168.192.in-addr.arpa";
		};
		```
		![vmlocal-conf2](assets/vmlocal-conf2.png)
	- Copykan file db.local pada path /etc/bind ke dalam folder jarkom yang baru saja dibuat dan ubah namanya menjadi 10.20.172.in-addr.arpa
		```bash
		sudo cp /etc/bind/db.local /etc/bind/vm/10.20.172.in-addr.arpa
		```
		*Keterangan 10.20.172 adalah 3 byte pertama IP VM yang dibalik urutan penulisannya*
	- Edit file 10.20.172.in-addr.arpa menjadi seperti gambar di bawah ini
		```bash
		sudo nano /etc/bind/vm/10.20.172.in-addr.arpa
		```
		![vmlocal-conf3](assets/vmlocal-conf3.png)
	- Kemudian restart bind9 dengan perintah
		```bash
		sudo service bind9 restart
		```
	- Rubah DNS wsl dengan ip wsl, dan beri comment pada default dns
		```bash
		sudo nano /etc/resolv.conf
		```
		![etc-resolv](assets/etc-resolv.png)
	- Untuk mengecek apakah konfigurasi sudah benar atau belum, lakukan perintah berikut 
		```bash
		sudo apt install dnsutils
		host -t PTR "IP VM"
		```
		![host-ptr](assets/host-ptr.png)
3. Record CNAME

	Record CNAME adalah sebuah record yang membuat alias name dan mengarahkan domain ke alamat/domain yang lain.
	- edit file /etc/bind/vm/vm.local
		```bash
		sudo nano /etc/bind/vm/vm.local
		```
		![cname](assets/cname.png)
	- Kemudian restart bind9 dengan perintah
		```bash
		sudo /etc/init.d/named restart
		```
	- Lalu cek dengan melakukan host -t CNAME www.vm.local atau ping www.vm.local. Hasilnya harus mengarah ke host dengan IP VM.
	![success](assets/success.png)
4. DNS Forwarder
	DNS Forwarder digunakan untuk mengarahkan DNS Server ke IP yang ingin dituju.
	- Edit file /etc/bind/named.conf.options
	- Uncomment pada bagian ini
		```bash
		forwarders {
		    8.8.8.8;
		};
		```
	- Comment pada bagian ini
		```bash
		// dnssec-validation auto;
		```
	- Dan tambahkan
		```bash
		allow-query{any;};
		```
		![dns forwarder](assets/dns-forwarder.png)
	- Kemudian restart bind9 dengan perintah
		```bash
		sudo service bind9 restart
		```
	- Harusnya jika nameserver pada file /etc/resolv.conf di client diubah menjadi IP WSL maka akan di forward ke IP DNS google yaitu 8.8.8.8 dan bisa mendapatkan koneksi.
5. Setting nameserver pada client
	- Untuk linux, mengganti dns hanya perlu merubah /etc/resolv.conf
	- Untuk Windows, ikuti step dibawah ini
		+ buka control panel
		+ pilih network and internet
		+ pilih network and sharing center
			![](assets/cp-1.png)
		+ pilih change adapter setting
			![](assets/cp-2.png)
		+ jikalau menggunakan wifi, silahkan click kanan -> properties pada wifi adapter, jikalau menggunakan lan, silahkan click kanan -> properties pada ethernet
			![](assets/cp-3.png)
		+ pilih internet protocol version (TCP/IPv4), lalu klik properties
			![](assets/cp-4.png)
		+ ganti dns dengan ip wsl 

			![](assets/cp-5.png)
		+ coba akses www.vm.local dan vm.local pada browser kesayangan anda
			![](assets/success-vmlocal.png)
		+ coba akses google.com dengan browser kesayangan anda
			![](assets/success-google.png)
		+ cek dns dengan cmd di windows
			```ps
			ipconfig/all
			```
			![](assets/cmd-dns.png)
		+ jika tidak bisa akes vm.local, silahkan kembali ke adapter wifi, dan uncheck internet protocol version (TCP/IPv6)

### References
* https://computer.howstuffworks.com/dns.htm
* http://knowledgelayer.softlayer.com/faq/what-does-serial-refresh-retry-expire-minimum-and-ttl-mean
* https://en.wikipedia.org/wiki/List_of_DNS_record_types
* https://kb.indowebsite.id/knowledge-base/pengertian-catatan-dns-atau-record-dns/
* https://github.com/arsitektur-jaringan-komputer/Modul-Jarkom-old/blob/master/Jarkom-2018-2/Modul2-DNS-dan-Webserver/DNS/README.md

------

## Soal Praktikum
1. buat subdomain dev.vm.local dengan menggunakan ansible dengan beberapa aturan:
	1. Menggunakan ansible
	2. menggunakan lxc yang sama dengan yang digunakan dengan vm.local
	3. folder code harus berbeda dengan yang digunakan vm.local, gunakan /var/www/html/dev/{nama_app}
2. Daftarkan subdomain vm.local ke DNS
3. responsi di minggu ke 11


