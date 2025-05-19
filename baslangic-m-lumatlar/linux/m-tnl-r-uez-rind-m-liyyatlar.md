---
description: Datanı istədiyimiz formaya salmaq
---

# Mətnlər üzərində əməliyyatlar

`sed`  -  (**S**tream **ED**itor) data axınları üzərində dəyişiklik edə biləcəyiniz bir əmr. Məsələn faylda olan 'windows' sözlərini 'linux' sözü ilə əvəz etmək istəyiriksə:

```
kali@kali:~$ sed -i 's/windows/linux/g' fayl_adi
```

Yalnız fayllarda deyil, keçən məqalələrdə olduğu kimi başqa bir əmrin verdiyi outputda da dəyişikliklər edə bilərik. Bunun üçün yazdığımız əmrdən sonra **piping** işlətməliyik.

`cut`  -  Datanı sütunlara görə bölmək üçün əmr. \
Deyək ki əlinizdə aşağıdakı kimi bir data var:

```
12.08.2020 16:55 192.168.0.103 /about.php
12.08.2020 17:20 192.168.0.102 /login.php
12.08.2020 17:35 192.168.0.108 /register.php
12.08.2020 18:22 192.168.0.110 /home.php
```

Əgər sizə burada olan yalnız IP adreslərin siyahısı lazımdırsa, belə olan halda aşağıdakı əmr bizim köməyimizə çata bilər:

```
kali@kali:~$ cat data | cut -d" " -f 3
192.168.0.103
192.168.0.102
192.168.0.108
192.168.0.110
```

Yuxarıda biz cat əmri köməkliyi ilə datamızı terminala çıxarıb sonra əmrləri bir birinə qoşmaqla (piping) ikinci əmri yerinə yetirdik. Əmrdə olan `-d`  -  delimiter (ayırıcı), `-f` - field (hissə) mənası daşıyır. Bununla da biz kodda gələn datadakı hər sətri boşluqlara əsasən (`-d" "`) hissələrə ayırmasını və alınmış 4 hissədən yalnız 3-cüsünü (`-f 3`) istədiyimizi bildirdik.

`awk` - bu mətnlər üzərində redaktə etmək üçün daha çox təkmilləşmiş bir əmrdir. Hətta belə demək olarsa, özünə məxsus proqramlaşdırma dili var. Aşağıda standart bir awk əmrini görə bilərsiniz.&#x20;

```
kali@kali:~$ awk '/axtarilan_ifade/ { ifade_uzerinde_emeliyyat; }' fayl_adi
```

Yuxarıdakı sintaksisə əsasən belə bir misal çəkək. Tutaq ki, əlimizdə aşağıdakı kimi adı **test** olan bir fayl var:

```
12.08.2020 16:55 192.168.0.103 /about.php
12.08.2020 17:20 192.168.0.102 /login.php
12.08.2020 17:35 192.168.0.108 /register.php
12.08.2020 18:22 192.168.0.110 /home.php
12.08.2020 17:35 192.168.0.106 /register.php
12.08.2020 16:55 192.168.0.103 /about.php
12.08.2020 17:20 192.168.0.102 /login.php
12.08.2020 17:35 192.168.0.110 /register.php
12.08.2020 18:22 192.168.0.110 /home.php
```

Əgər biz bu faylda **/register** endpointinə daxil olmuş ip addresslərini görmək istəyiriksə, belə olan halda aşağıdakı kimi əmr yazmaq işimizə yarayacaqdır:

```
kali@kali:~$ awk '/register/ {print $3;}' test
192.168.0.108
192.168.0.106
192.168.0.110
```

1-ci sətrdə də göründüyü kimi `awk` əmrini istifadə edərək əvvəlcə **test** faylının içərisində register ifadəsi olan sətirləri seçməsini istədik - `/register/` . Buna görə də 3 sətir seçdi. Sonra isə biz yalnız IP adreslərin seçilməsi üçün seçilən cümlələrin hər birinin 3-cü hissəsini print etməsini istədik - `{print $3;}`. Niyə məhz 3? AWK əmri default (standart) olaraq seçdiyi hissələri boşluqlara əsasən hissələrə ayırır. Eynən aşağıda olduğu kimi:

```
   | 1 |    |2|       |3|          |4|
12.08.2020 17:35 192.168.0.106 /register.php
```

İndi isə biz IP adreslərlə yanaşı tarixi də görmək istəyiriksə onda deməli bizə 3-cü hissə ilə yanaşı həm də 1-ci hissə də lazımdır. İlk yazdığımız awk əmrini aşağıdakı kimi dəyişməklə məqsədimizə nail ola bilərik:

```
kali@kali:~$ awk '/register/ {print $1,$3;}' test
12.08.2020 192.168.0.108
12.08.2020 192.168.0.106
12.08.2020 192.168.0.110
```

