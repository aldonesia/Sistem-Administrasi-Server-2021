# FINAL PROJECT SISTEM ADMINISTRASI SERVER 2021/2022

## Jalan Cerita

Stephanie dan Gede terpilih menjadi junior SysAdmin di salah satu BUMN pada program Magang Kampus Merdeka. Mereka ditugaskan untuk mendeploy website yang akan di launching 2 minggu lagi. Senior SysAdmin mereka yang bernama Sung Jin-Woo memberikan beberapa penjelasan dan masukan terkait persiapan yang dibutuhkan.

Terdapat 4 website yang akan di deploy

1. kelompokXX.fpsas/ menggunakan framework laravel 8 dan php 7.4
2. news.kelompokXX.fpsas menggunakan framework wordpress terbaru dan php 7.4
3. kelompokXX.fpsas/product menggunakan framework yii 2.0 dan php 7.4
4. kelompokXX.fpsas/app menggunakan framework codeigniter 3 dan php 5.6

## Teknologi yang digunakan

teknologi yang digunakan antara lain

1. VM Ubuntu 20.04 (menggunakan metode bridge network, dan static ip)
2. Nginx
3. 6 instance LXC ubuntu 20.04 PHP 7.4
4. 2 instance LXC debian 10 PHP 5.6
5. 1 instance LXC debian 10 mariadb server
6. Semua instalasi menggunakan Ansible
7. kelompokXX.fpsas/ menggunakan laravel 8
8. news.kelompokXX.fpsas menggunakan wordpress terbaru
9. kelompokXX.fpsas/product menggunakan YII 2.0
10. kelompokXX.fpsas/app menggunakan Code Igniter 3

## Arsitektur Jaringan

![](assets/arsitektur.png)

Setiap website memiliki load balancer ke beberapa instance lxc

1. kelompokXX.fpsas/
	1. Menggunakan metode load balancer Least Connection 4 instance LXC, antara lain LXC_PHP7_1, LXC_PHP7_2, LXC_PHP7_4, LXC_PHP7_6
2. news.kelompokXX.fpsas
	1. Menggunakan metode load balancer Ip Hash 4 instance LXC, antara lain LXC_PHP7_2, LXC_PHP7_3, LXC_PHP7_4, LXC_PHP7_5
3. kelompokXX.fpsas/product
	1. Menggunakan metode load balancer Weighted Load Balancing 5 instance LXC, antara lain LXC_PHP7_1 (Weight=3), LXC_PHP7_2 (Weight=2), LXC_PHP7_4 (Weight=4), LXC_PHP7_5 (Weight=1), LXC_PHP7_6 (Weight=6)
4. kelompokXX.fpsas/app
	1. Menggunakan metode load balancer Round Robin 2 instance LXC, antara lain LXC_PHP5_1, LXC_PHP5_2
	
Database Server terpusat menggunakan lxc debian 10 dengan nama LXC_DB_SERVER 

## Analisa Performa Arsitektur

Sung Jin-Woo memberikan tugas kepada stephanie dan gede untuk melakukan loadtest dengan beberapa variasi jumlah user dari 50, 150, 300, 500 untuk mendapat nilai rata - rata  througput dan rata-rata jumlah user yang dapat dilayani setiap detik untuk setiap website.

## Soal Analisa

1. Berapa nilai rata - rata througput untuk setiap website yang dihasilkan dari load testing?
2. Berapa nilai rata - rata jumlah user yang dapat dilayani setiap detik untuk setiap website yang dihasilkan dari load testing?
3. Bagaimana cara mengurangi nilai througput dan meningkatkan nilai jumlah user yang dapat dilayani setiap detik untuk skema yang telah dibuat ? Sebutkan faktor faktor yang mempengaruhi !


## Pengumpulan Final Project

Link Dokumentasi dan konfigurasi ansible diupload ke github dan url github di kirim ke elearning maksimal 30 Januari 2022 pukul 20.22

## Penilaian dan Demonstrasi Final Project

Demonstrasi final project akan dilakukan mulai senin tanggal 31 Januari 2022 hingga selesai

Penilaian meliputi:

1. Konfigurasi Ansible (Semakin Otomatis semakin bagus, tidak ada konfigurasi manual)
2. Hasil dan Jawaban Analisa
3. Presentasi (Minggu 17, Jadwal Menyusul) dan Dokumentasi


## Referensi Instalasi

1. Modul 1, Modul 2, Modul 3, Modul 4
2. https://laravel.com/docs/8.x/installation
3. https://www.yiiframework.com/doc/guide/2.0/en/start-installation
4. https://www.codeigniter.com/userguide3/installation/index.html
5. https://wordpress.org/support/article/how-to-install-wordpress/

## MEMEs

![](assets/final-project-final-project-everywhere.jpg)

![](assets/Final-project-requirements-vs-What-students-turn-in-meme-7642.jpg)