---
title: "Homework 4 : Game Architecture"
excerpt: ""
collection: blog
---


<br>
<center><img style="margin-top:2%; margin-bottom:2%" src='/images/class_diagram.png'></center>
<br>

<p align="justify">Gambar di atas menggambarkan class diagram GOIndonesia. Kami membentuk 3 sub package di dalam package utama, yaitu scenes, screens, dan sprites. Package scenes dibuat untuk menampilkan sesuatu yang ada di layar pada saat game dimainkan, yaitu HUD (Head Up Display) dan Controller. Package screens dibuat untuk menampilkan setiap screen yang ada di dalam game, misalnya MainMenu, GameOver, LevelSatu, LevelDua, dst. Package sprite dibuat untuk menambahkan sprite ke dalam game, misalnya player (Garuda), enemy, koin, dst. Kemudian untuk meload setiap asset yang ada akan dilakukan pada class GOIndonesia dan menset screen pertama yang akan ditampilkan.</p>