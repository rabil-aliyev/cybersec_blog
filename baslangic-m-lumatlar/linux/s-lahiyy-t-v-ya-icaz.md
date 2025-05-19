---
description: Privilege  /  Permission
---

# Səlahiyyət və ya İcazə

Linuxda hər-hansı fayl ilə bağlı əmr icra olunması üçün buna əvvəlcə istifadəçinin səlahiyyəti olmalıdır. Bu səlahiyyət istifadəçinin birbaşa özünə və ya mənsub olduğu qrupa verilə bilər. Məsələn `passwd` faylı linuxda olan bütün istifadəçilər tərəfindən default olaraq oxuna bilir. Yəni bu faylı oxumaq üçün hər kəsin səlahiyyəti var. shadow faylı haqqında daha əvvəlki məqalədə məlumat vermişdim. İndi isə shadow faylını terminalda görüntüləməyə çalışaq:

```
kali@kali:~$ cat /etc/shadow
cat: /etc/shadow: Permission denied
```

Yuxarıda gördüyünüz kimi bizə icazəmizin olmadığı ilə bağlı xəta outputu göstərdi. Çünki shadow faylı həssas fayllardan biridir və hamı tərəfindən əlçatan deyil. Linuxda ən üstün səlahiyyətə malik olan istifadəçi `root` adlı istifadəçidir. Bir çox əmrlər var ki, onların icrası mütləq root səlahiyyətini tələb edir. `shadow` faylı da həmçinin yalnız `root` tərəfindən əlçatandır. Lakin heç də hər zaman root olmağa ehtiyyac yoxdur. `sudo` əmri hərhansı bir əmrin başqa istifadəçi tərəfindən icra edilməsini təmin edir. Bu əmri istifadə edərək biz özümüzə lazım olan əmri root səlahiyyətlərii ilə yerinə yetirə bilərik. Linuxda bir istifadəçinin sudo əmrini istifadə edə bilməsi üçün onun adının və ya mənsub olduğu qrupun adının `/etc/sudoers` faylında olmağı lazımdır. Standart olaraq Kali Linuxda olan `kali` adlı istifadəçi `sudo` adlı qrupa daxildir. Və sudo qrupunun adı `sudoers` faylında var. Ona görə də biz  kali adlı istifadəçimizlə sudo əmrini istifadə edə biləcəyik.

Yuxarıda səlahiyyətimizin çatmaması ilə bağlı aldığımız xəta mesajını indi almadan `shadow` faylını oxumağa cəhd edək. Lakin bu dəfə `sudo` əmri ilə:

```
kali@kali:~$ sudo cat /etc/shadow
[sudo] password for kali:
root:$6$Qx43qZBHZkxeSdas45d5as4da65s4d2pTqfJ1:18515:0:99999:7:::
daemon:*:18390:0:99999:7:::
bin:*:18390:0:99999:7:::
colord:*:18390:0:99999:7:::
geoclue:*:18390:0:99999:7:::
lightdm:*:18390:0:99999:7:::
king-phisher:*:18390:0:99999:7:::
kali:$6$BiEAYF4pzDp5QJXH$00iURpImugngJWduN2XgIjtTicF720:18390:0:99999:7:::
systemd-coredump:!!:18390::::::
debian-tor:*:18457:0:99999:7:::
i2psvc:*:18457:0:99999:7::1:
user24:!:18472:0:99999:7:::
user241:!:18472:0:99999:7:::
user77:$6$biiBhwpN2XvpEyeOFZNfia9/NpInGq9emZkkVERKF8MRqrljqM.:18472:0:99999:7:::
marcus_user:!:18475:0:99999:7:::
root2:!:18476:0:99999:7:::
rabil:!:18496:0:99999:7:::
shareuser:$6$firpdq8h.f2U6PnsFMfffyijaK5ftnKIe4dd1:18530:0:99999:7:::
ftpuser:!:18504:0:99999:7:::
Debian-exim:!:18508:0:99999:7:::
uuidd:*:18508:0:99999:7:::
sddm:*:18575:0:99999:7:::
xrdp:!:18587:0:99999:7:::
redis:*:18594:0:99999:7:::
```

Gördüyünüz kimi **2-ci** sətirdə bizdən şifrəmizi yazmağımız tələb etdi. Şifrəmizi yazdıqdan sonra artıq daha yüksən səlahiyyəti istifadə edə bilərik. Bununla da parolların şifrələnmiş halı bizim üçün əlçatandır.

### Fayl və Qovluq icazələri (File and Directory permissions)

Kali Linux əməliyyat sistemində fayl və qovluqların icazələrinə `ls -la` əmri vasitəsilə baxmaq olar. \
**ls**  -  qovluq içərisində olan faylları görüntüləmək\
&#xNAN;**-l**  -  əmrin geniş formada output verməyini təmin etmək\
&#xNAN;**-a**  -  bütün faylları göstərmək (Nöqtə ilə başlayan fayllar normalda görünmür, bu əmrlə baxmaq olar)

kali adlı istifadəçimizə məxsus olan `/home/kali/` qovluğunda yuxarıdakı əmri daxil edərək faylları və onların icazələrini görməyə çalışaq:

```
kali@kali:~$ ls -la
total 8
drwxr-xr-x 2 kali kali     4096 Jul 29 19:09 .
drwxr-xr-x 7 root root     4096 Aug 22 11:57 ..
-rw-r--r-- 1 kali kali      220 Jul 29 19:09 .bash_logout
-rw-r--r-- 1 kali kali     3391 Jul 29 19:09 .bashrc
-rw-r--r-- 1 kali kali     3526 Jul 29 19:09 .bashrc.original
drwx------ 2 kali kali     4096 Aug 12 11:03 .ssh
-rw-r--r-- 1 kali kali      807 Jul 29 19:09 .profile
-rwxrwxrwx 1 kali kali       18 Dec 17 11:35 hamiUchun.txt
```

Yuxarıda gördüyünüz kimi hər sətrin ilk 10 simvolu ilk baxışdan anlaşılmayan hərflərlə sanki kodlaşdırılmış şəkildə yazılıb. Linux əməliyyat sistemində fayl və qovluq icazələri məhz bu şəkildə işarə edilir. İndi həmin fayllardan birinin ilk 10 simvolunu götürüb onların nə mənaya gəldiyiniz izah etməyə çalışaq.

### -rwxrw-r--

Yuxarıda gördüyünüz 10 simvolun ilk hərfi obyektin qovluq yoxsa fayl olub olmadığını müəyyən edir. Əgər qovluq olarsa orada tire (**-**) əvəzində **d (directory)** hərfini görəcəkdik. Belə: **drwxrw-r--**

Qalan 9 simvoly aşağıdakı kimi 3 qrupa bölə bilərik.

| 1ci hissə | 2-ci hissə | 3-ci hissə |
| --------- | ---------- | ---------- |
| rwx       | rw-        | r--        |

İlk hissədə olan 3 simvol (rwx) faylın sahibinə aid icazələrini göstərir. Belə ki faylın yaradıcısı bu faylı\
**r -** oxuya **(r**ea&#x64;**)**\
**w -** yaza və ya dəyişdirə (**w**rite)\
**x -** icra edə (e**x**ecute) bilər.  \
Əgər bu səlahiyyətlərdən biri olmazsa, belə olan halda hərf əvəzinə tire yazılır. Məs. yazmaq olmazsa: r-x

Ikinci hissə istifadəçinin mənsub olduğu qrup üzvlərinə aid icazələri göstərir. Yuxarıda misal çəkdiyimiz faylın yaradıcısının mənsub olduğu qrupun üzvləri bu faylı oxuya və yaza bilsələr də icra edə bilmirlər **(rw-).**

Üçüncü hissə faylın digərlərə uyğun olan icazələrini göstərir. Yəni bir istifadəçi əgər yuxarıda gördüyünüz icazələrə sahib olan faylın yaradıcısı deyilsə, və yaradıcısı ilə eyni qrupda deyilsə belə olan halda yalnız oxuya biləcək **(r--).**&#x20;

### **İcazələri dəyişmək**

Kali Linuxda bir fayla aid icazələrdə dəyişiklik etmək üçün `chmod` əmri istifadə edilir. Məsələn bir faylı hamı tərəfindən oxuna bilən etmək üçün `chmod +r` əmri istifadə oluna bilər. Burada +r ifadəsini \
"**r** əlavə et" kimi başa düşmək olar.

```
kali@kali:~$ chmod +r fayl.txt
kali@kali:~$ ls -la
-rwxr--r--  1 kali kali    18 Dec  7 12:18 test
```

Göründüyü kimi icazələr olan ilk 10 simvolun hər üç qrupunda **r** hərfi var. Bu da onun artıq hərkəs tərəfindən oxunabilən olduğunu bildirir. Yuxarıdakı əmri həmçinin **+x** və **+w** ilə yazaraq hamı üçün icra edilə bilən və hamı tərəfindən yazılabilən etmək olar.&#x20;

Linux icazələri həmçinin rəqəmlərlə də işarə oluna bilər. Aşağıdakı kimi.&#x20;

* 0 = ---
* 1 = --x
* 2 = -w-
* 3 = -wx
* 4 = r-
* 5 = r-x
* 6 = rw-
* 7 = rwx

Bəs bu rəqəmlər necə istifadə edilir? \
chmod əmrinin köməyi ilə.  Məsələn əgər biz yaratdığımız bir skriptin bizim tərəfimizdən oxuna, yazıla və icra edilə bilən olmasını istəyiriksə belə olan halda bizə **7** və **0** rəqəmi lazımdır. Çünki yuxarıdakı cədvəldən də göründüyü kimi **7** rəqəminin qarşılığı özündə oxumağı, yazmağı və icra olunmağı birləşdirir. **0** rəqəmi isə heç bir icazəni əks etdirmir. Deməli biz ilk qrupa **7**, qalan iki qrupa isə **0** nömrəli səlahiyyətləri verməliyik. Beləliklə biz aşağıdakı əmri yazmaqla bir faylı yalnız özümüz tərəfindən əlçatan edə bilərik:

```
kali@kali:~$ chmod 700 script.py
kali@kali:~$ ls -la
-rwx------  1 kali kali    18 Dec  7 12:18 script.py
```

Göründüyü kimi ilk qrupda bütün səlahiyyətlər açıq olsa da digər qruplarda heç biri açıq deyil. Skripti hamı üçün oxuna, yazıla və icra edilə bilən etmək istəsək:&#x20;

```
kali@kali:~$ chmod 777 script.py
kali@kali:~$ ls -la
-rwxrwxrwx  1 kali kali    18 Dec  7 12:18 script.py
```

Hər üç qrupa 7 nörməli icazəni tətbiq edərək skripti hamı üçün əlçatan etdik.
