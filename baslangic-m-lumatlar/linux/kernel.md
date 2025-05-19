---
description: Nüvə
---

# Kernel

Kernel, qurğular (hardware) və proqram təminatı (software) arasında əlaqə quran və sistem resurslarını idarə edən, ən alt səviyyədə çalışan program təminatıdır. Kerneli fayl olaraq /boot qovluğu içərisində tapmaq olar. Lakin buna root səlahiyyətləri lazımdır. Buna görə də sudo!

```
kali@kali:~$ sudo ls -la /boot/
[sudo] password for kali: 
total 73524
drwxr-xr-x  3 root root     4096 Nov 21 06:14 .
drwxr-xr-x 20 root root    36864 Aug 30 12:41 ..
-rw-r--r--  1 root root   226403 Apr 21  2020 config-5.5.0-kali2-amd64
drwxr-xr-x  5 root root     4096 Nov 21 06:12 grub
-rw-------  1 root root 65098427 Nov 21 06:14 initrd.img-5.5.0-kali2-amd64
-rw-r--r--  1 root root  4141267 Apr 21  2020 System.map-5.5.0-kali2-amd64
-rw-r--r--  1 root root  5761408 Apr 21  2020 vmlinuz-5.5.0-kali2-amd64
```

Başlanğıcda kernel sadəcə linux adlanırdı. Ancaq ilk Virtual Yaddaş təqdim edildikdən sonra kernelin virtual yaddaşla işləyə biləcəyini göstərmək üçün adını vmlinux olaraq dəyişdirdilər. Daha sonra kernel çox böyüdükdə **zlib** istifadə edilərək sıxıldı, buna görə də adı **vmlinuz** olaraq dəyişdirildi. Linux Kernel, Windows-dan həmçinin standart olaraq sürücülərin (driver) üzərində gəlməsi ilə fərqlənir. Beləliklə, bir printer və ya bənzər bir şey qurmaq istədiyiniz zaman, Windows-da olduğu kimi sürücü axtarmağa ehtiyac yoxdur.

Linux kernel hər yeni boşluq aşkarlandıqca və ya inkişaf etdikcə yenilənir. Bu yeniləmələri əldə etmək çox asandır. Aşağıdakı əmrlərdən hər hansı biri vasitəsilə linux kerneli yeniləmək olar:

```
sudo apt-get update && sudo apt-get dist-upgrade
sudo apt-get update && sudo apt-get upgrade
```
