---
description: FileSystem
---

# Qovluq quruluşu

Windowsda fayllar disklərdə olduğu halda linux əməliyyat sistemində bunlar partition adlanır. Kali linux sistemində komponentlər aşağıdakı şəkildə qovluqlara ayrılıb:

1. /bin/ — sadə programlar (`ls`, `cd`, `cat`, `etc`.)&#x20;
2. /sbin/ — sistem programları (`fdisk`, `mkfs`, `sysctl`, `etc`)
3. &#x20;/etc/ — konfiqurasiya faylları
4. &#x20;/tmp/ — müvəqqəti fayllar
5. /usr/bin/ —istifadəçi  tətbiq və ya alətləri (`apt`, `ncat`, `nmap`, `etc`.)
6. /usr/share/ — istifadəçi tətbiq və ya alətlərə məxsus fayllar
7. /dev/ - qurğulara aid fayllar
8. /home/ - istifadəçilər üçün avtomatik yaradılan qovluqlar. (Məs.: **`/home/kali`**)
9. /lib/ - Kitabxanalar və Kernel modulları
10. /opt/ - Sonradan yüklənilən istəyə bağlı program və ya paketlər
11. /var/ - Dəyişkən data faylları

